After downloading the Mac distribution:

1. Open Terminal. You can do this by pressing Cmd + Space, typing Terminal, and hitting Enter.

2. Navigate to the Downloads folder (or the folder where you saved the file) by typing this in Terminal:

cd ~/Downloads

3. Remove the quarantine attribute. Run the following command to allow the app to launch properly by typing this in Terminal:

xattr -dr com.apple.quarantine iperf3-GUI.app

4. Launch the app. You can now double-click iperf3-GUI.app in Finder.
