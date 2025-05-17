* **`buildapp-linux.py` Usage**

  `buildapp-linux.py` is a script to quickly build ProperTree as an app. It goes through each required ProperTree asset to bundle it all in one file that can be ran anywhere. There are also several arguments you can use to customize it, as shown below.

    - `--verbose` or `-v`: Run the script in verbose mode. This shows extra logs that may be helpful for debugging.
    - `--python "*"` or `-p "*"`: Add this argument and replace `*` with a Python executable to use it for ProperTree. If this argument is not included, then the output is taken from `which python3`. (You will have to overwrite this if you wish to use Python 2 with ProperTree, as it defaults to the Python 3 executable. This is because `python` is sometimes not included with Python.)
    - `--clear` or `-c`: Clear `dist/linux`. This does not respect `--use-existing-payload`.
    - `--always-overwrite`: Don't ask if you want to overwrite `settings.json` in `/home/user/.ProperTree` (if it exists). This argument will force the script to overwrite it no matter what.
    - `--use-existing-payload`: For debugging purposes only. This makes it so the script doesn't delete `dist/linux/payload` and instead uses it for the next run.
    - `--skip-compile`: Don't use `gcc` to compile into an executable, but instead skip that step.

  `buildapp-linux.py` puts all results in `dist/linux/result`, relative to the current Python directory. It will generate three files: `ProperTree`, `ProperTree.sh`, and `ProperTree-Installer-V.sh`.
    - `ProperTree` is the (optional) ELF executable generated. It's simply a wrapper around `ProperTree.sh`. It requires `gcc` to be installed and the `--skip-compile` argument to not be present. The executable currently only support x64, but the provided `main.c` in `dist/linux` can be compiled manually to any architecture. This accepts the same arguments as `ProperTree.sh`.
    - `ProperTree.sh` is the containing script for ProperTree. It simply extracts its included payload to `/tmp/.ProperTree`, then runs the extracted `ProperTree.py`. **Note**: Run this script with `--clear-data` to remove ProperTree data.
    - `ProperTree-Installer-V.sh`: This script places 2 shell scripts in `/home/user/.local/bin` and a `ProperTree.desktop` file in `/home/user/.local/share/applications`. The 2 shell scripts in `.local/bin` are `ProperTree` and `propertree` (the latter just points to `ProperTree`). This is so case doesn't matter when running ProperTree from the command line. You can also run this with `--uninstall` to uninstall ProperTree without clearing your data. (You can clear data with `ProperTree.sh` using `clear-data`.
  
  **Notice**: ProperTree uses `/home/user/.ProperTree` for ProperTree data. Don't delete any of the files in this directory manually; they can be deleted using the scripts above.
  
  For more info on this script, including what different files do and known issues, [check it out directly](https://github.com/corpnewt/ProperTree/blob/master/Scripts/buildapp-linux.py). There is a lot of documentation at the top of the script.
