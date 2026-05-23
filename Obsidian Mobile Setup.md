- install obsidian mobile and create a `test_vault`
- install `ish` app
- run this command `apk add git`
- check git version `git --version`
- run this cmd to create a folder `mkdir system_design_obsidian`
- next mount the folder that you created using cmd `mount -t ios . system_design_obsidian/`
  opens the file explorer and choose just the main Obsidian folder
- then go inside the mounted folder using `cd system_design_obsidian/`
- then run this `ls` command to see(`test_vault`) test obsidian vault that you have created
- After confirmation clone into repo using cmd`git clone https://github.com/kranthikumarkaranam/system_design_obsidian.git`
- then run same `ls` command to see two vaults
  1. `test_vault`
  2. `system_design_obsidian`
- then again go inside the cloned directory by `cd system_design_obsidian`
- now check the `git status`
- then run this cmd to remove those git errors`git config --global --add safe.directory /root/system_design_obsidian/system_design_obsidian`