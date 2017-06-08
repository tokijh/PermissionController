# PermissionController
Permission Controller

## 권한 체크 및 획득 순서
1. 따로 패키지를 만든후 `PermissionController`와 `PermissionControllerActivity`를 가진다.
2. `check`를 하면 권한 체크 및 획득을 한다. 이때 `PermissionCallback`을 받아 결과에 대해서 처리한다.
3. `PermissionController`에서 버전에 따라 권한 획득 처리를 해준다.
4. RuntimePermissionCheck가 필요한 경우 `PermissionControllerActivity`를 실행한다.
5. `PermissionControllerActivity`는 onStart되자마자 `requestPermissions`를 한다.
6. `PermissionControllerActivity`에서 `onRequestPermissionsResult`가 처리 결과를 받고 이를 `PermissionController`에서의 마지막 데이터와 (`static PermissionController permissionController`)에서 각 필요한 데이터와 메소드를 불러와 처리한다.

## PermissionCallback
    void success();
    void error();

## 사용 방법
`AndroidManifast.xml`에서 아래 코드를 추가한다.

```
<activity android:name=".Permission.PermissionControllerActivity" />
```

권한체크를 해야 하는 곳에서 아래 예제를 참고하여 진행 한다.

```
new PermissionController(this,
    new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE
            , Manifest.permission.CAMERA})
            .check(new PermissionController.PermissionCallback() {
                @Override
                public void success() {
                    Logger.d("TAG", "success");
                }

                @Override
                public void error() {
                    Logger.d("TAG", "error");
                }
            });
```
