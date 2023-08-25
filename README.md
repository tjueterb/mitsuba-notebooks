# Mitsuba Notebooks

This is a Work in Progress repository for the development of the acoustic path tracing branch. It contains jupyter notebooks for in-depth understanding and scenes for debugging.

Tips for debugging in VS Code:

- Install the Cmake Tools extension
- Compile Mitsuba3 in the Debug configuration
- For debugging the `simple_spectral.xml` scene in VS Code, add this to your `launch.json`:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug spectral scalar",
            "type": "cppdbg",
            "request": "launch",
            // Resolved by CMake Tools:
            "program": "${command:cmake.launchTargetPath}",
            "args": ["-v",
            "-m", "scalar_spectral", //use Scalar Spectral variant
            "--threads", "1", // use only one thread
            "notebooks/scenes/simple_spectral.xml"], // change this to the correct path
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            // "miDebuggerPath": "/usr/bin/gdb",
            "environment": [
                {
                    // add the directory where our target was built to the PATHs
                    // it gets resolved by CMake Tools:
                    "name": "PATH",
                    "value": "$PATH:${command:cmake.launchTargetDirectory}"
                },
                {
                    "name": "OTHER_VALUE",
                    "value": "Something something"
                }
            ],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        },
    ]
}
```
