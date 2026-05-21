

> 💡 **Why entity ranges are the recommended**?
>
> Entity ranges store the text exactly once and keep metadata separately.
>
> Example:
>
> ```json
> {
>   "text":"Check out @greatfrontend at https://www.greatfrontend.com #webdev",
>   "entities":[
>     {
>       "type":"mention",
>       "start":10,
>       "end":24,
>       "userId": "u_99"
>     },
>     {
>       "type":"link",
>       "start":28,
>       "end":57,
>       "url": "https://www.greatfrontend.com"
>     },
>     {
>       "type":"hashtag",
>       "start":58,
>       "end":65
>     }
>   ]
> }
> ```
>
> Benefits:
>
> - Compact → text stored only once
> - Platform agnostic → works for Web, iOS, Android
> - Easy to render → slice text and decorate ranges
> - Easy to extend → mentions, hashtags, links, emojis
>
> Rendering:
>
> ```js
> text.slice(10,24)
> // "@greatfrontend"
> ```
>
> ---
>
> **Editing caveat**
>
> Entity ranges are good for storage but awkward for editing.
>
> Before:
>
> ```txt
> Check out @greatfrontend
>           ^------------^
>            start=10 end=24
> ```
>
> User inserts:
>
> ```txt
> Check this out @greatfrontend
> ```
>
> Now all indexes shift:
>
> ```txt
> start=15
> end=29
> ```
>
> Every insertion/deletion forces later ranges to update.
>
> ---
>
> **Real editor approach**
>
> Rich-text editors (Lexical, TipTap, Slate) keep a richer internal tree:
>
> ```txt
> Document
> ├── Text("Check out ")
> ├── Mention("@greatfrontend")
> └── Hashtag("#webdev")
> ```
>
> Editing becomes easy because nodes change instead of character indexes.
>
> Before sending data to API:
>
> ```txt
> Rich tree
>     ↓ serialize
> Entity ranges
> ```
>
> *Store/send entity ranges. Edit with a richer tree model.*
