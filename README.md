# Auto Update Module

This module streamlines the addition of auto-update functionality. This file should be added to the main folder of your script, or the folder of the file that will be referencing the module.

These lines should be added to the top of the script with other module imports.

    import AutoUpdate
    from AutoUpdate import COLOUR      # Colour class allows the module to output colour to to the terminal 

This code should be added to the top of the main function of the tool so that it runs at the very beginning of the script:

    ### main function
    exe_name = os.path.basename(__file__)
    local_dir = os.path.dirname(__file__)
    local_version = AutoUpdate.get_local_version(exe_name)
    if local_version == None:
        local_version = "v.undefined"
        print(f"\n{COLOUR.RED}Local version could not be determined - could not check for updates.\nCurrent version may be outdated. Please contact Jake or Kai.\n")
    else:
        url = "https://api.github.com/repos/GITHUB USERNAME/REPO NAME/contents/releases" ### CHANGE THIS TO REPO URL
        latest_version = AutoUpdate.get_latest_version(url)
        if latest_version is None:
		        print(f"\n{COLOUR.RED}Could not check for updates, please restart tool.\nIf issue persists contact Jake or Kai.\n")
        else:
            download_url = f"https://raw.githubusercontent.com/GITHUB USERNAME/REPO NAME/main/releases/TOOL NAME_{latest_version}.exe" ### CHANGE THIS TO REPO URL
            AutoUpdate.check_for_updates(local_version, local_dir, latest_version, download_url)
    ### rest of code...

The code in capitals (excluding calls of 'COLOUR' class) should be replaced with either your GitHub username, repo name, or tool name 
