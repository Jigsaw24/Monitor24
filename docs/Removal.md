# Removal / Uninstall

1. Remove any configuration profile configuration Monitor24.
2. Unload Monitor24

```
launchctl unload /Library/LaunchDaemons/com.jigsaw24.Monitor24.plist
```

3. Delete the App

```
rm -r /Applications/Monitor24.app
```

4. Delete Database Files

```
rm -r /Library/Application\ Support/Jigsaw24/Monitor24*
```

5. Delete LaunchDaemon

```
rm /Library/LaunchDaemons/com.jigsaw24.Monitor24.plist
```
