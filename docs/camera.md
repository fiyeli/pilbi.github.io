# Camera

This module provides a script that takes a 1024x768 picture using a Raspberry Pi Camera. The picture's name is a timestamp from the moment it was taken, ans it is stored in the folder given by the FIYEL_IMAGES environment variable.

## Dependencies

The module requires the picamera Python module to work.
```
pip install picamera
```

## Execution

```
python camera.py
```