# Gyroscope Camera Template

_优化了一下官方例程……而已……_

## 版本

- [Release 1.0](https://github.com/JadMax/JadMax.github.io/blob/master/unipacks/GyroscopeCamera.unitypackage) _2019年8月17日18:58:01_

## 核心脚本 CameraPreference.cs 

附在目标 Camera 上。

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class CameraPreference : MonoBehaviour
{
    public Toggle flipX;
    public Toggle flipY;
    public Toggle flipZ;
    public Toggle flipW;

    public bool isXFlipped = false;
    public bool isYFlipped = false;
    public bool isZFlipped = true;
    public bool isWFlipped = true;
    private void Start()
    {
        Input.gyro.enabled = true;
        Input.compensateSensors = true;
        Input.gyro.updateInterval = 0.01f;
    }
    private void Update()
    {
        flipX.isOn = isXFlipped;
        flipY.isOn = isYFlipped;
        flipZ.isOn = isZFlipped;
        flipW.isOn = isWFlipped;

        GyroCamera();
    }

    private void GyroCamera()
    {
        float nx = isXFlipped ? Input.gyro.attitude.x : -Input.gyro.attitude.x;
        float ny = isYFlipped ? Input.gyro.attitude.y : -Input.gyro.attitude.y;
        float nz = isZFlipped ? Input.gyro.attitude.z : -Input.gyro.attitude.z;
        float nw = isWFlipped ? Input.gyro.attitude.w : -Input.gyro.attitude.w;

        transform.localRotation = new Quaternion(nx, ny, nz, nw);
    }

    public void FlipX()
    {
        isXFlipped = !isXFlipped;
    }
    public void FlipY()
    {
        isYFlipped = !isYFlipped;
    }
    public void FlipZ()
    {
        isZFlipped = !isZFlipped;
    }
    public void FlipW()
    {
        isWFlipped = !isWFlipped;
    }
}
```

###### [返回主页](index.md)
