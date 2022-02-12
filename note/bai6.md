# Bài 6: Form

- Nội dung bài học:
    - Làm việc với Form
    - Kiểm lỗi Form (Validation)

## 1. Làm việc với Form
### 1.1. `ng-model`
- Sử dụng `ng-model` để ràng buộc dữ liệu với các input.
- `ng-model` sẽ thực hiện ràng buộc 2 chiều (2 way binding):
    - Chiều thứ nhất: lấy dữ liệu bên trong $scope & hiển thị lên giao diện.
    - Chiều thứ hai:  lấy dữ liệu người dùng nhập vào trên giao diện (input) & cập nhật vào trong $scope.
- Nếu trong $scope chưa có thuộc tính thì sẽ tự động tạo mới thuộc tính đó.

Ví dụ:

View:
```
<input type="text" name="fullname" ng-model="fullname">
```

Controller:
```
function myController($scope) {
    $scope.fullname = "Nguyễn Văn A";
}
```

### 1.2. `ng-model-options`
- Chỉ thị `ng-model-options` quy định cách thức cập nhật dữ liệu vào $scope (chiều thứ 2).

Ví dụ:
```
<input type="text" name="fullname" ng-model="fullname" ng-model-options="{ updateOn: 'blur' }">
```

- Sự kiện `blur` là sẽ được kích hoạt khi input mất con trỏ (mất focus).
- Ngoài sự kiện `blur`, có thể chỉ định các sự kiện khác: `click`, `mouseup`, `focus` ...
- Tham khảo: https://docs.angularjs.org/api/ng/directive/ngModelOptions

- Ngoài thuộc tính `updateOn`, có thể sử dụng `debounce` để setup thời gian cập nhật:
```
<input type="text" name="fullname" ng-model="fullname"
    ng-model-options="{ updateOn: 'blur', debounce: 1000 }">
```
=> Sau 1000ms (1s) sẽ cập nhật dữ liệu vào $scope

### 1.3. Checkbox & Radio
- Sử dụng `ng-model` để ràng buộc trạng thái của **radio** & **checkbox** vào thuộc tính trong $scope.

- Với **checkbox**:
```
<input type="checkbox" ng-model="remember_me">
<label>Ghi nhớ đăng nhập</label>
```

- Trong ví dụ trên, nếu checkbox được chọn -> thuộc tính *remember_me* trong $scope sẽ có giá trị `true`.
Ngược lại, *remember_me* sẽ có giá trị `false`.

- Với **radio**:
```
<input type="radio" ng-model="gioi_tinh" value="1"> <label>Nam</label>
<input type="radio" ng-model="gioi_tinh" value="0"> <label>Nữ</label>
```

- Trong ví dụ trên với **radio**, `$scope.gioi_tinh` sẽ có giá trị **1** nếu người dùng chọn *Nam*
    hoặc **0** nếu người dùng chọn *Nữ*.

- Ngoài ra, có thể sử dụng chỉ thị `ng-checked` để ràng buộc điều kiện: có chọn radio/checkbox hay không:
```
<input type="checkbox" ng-model="remember_me" name="remember_me"
    ng-checked="remember_me == 1" >
<label>Ghi nhớ đăng nhập</label>
```

### 1.3. Select
- Sử dụng `ng-model` để ràng buộc dữ liệu của `select` vào trong `$scope`.
- Sử dụng `ng-repeat` hoặc `ng-options` để đổ dữ liệu vào các thẻ `option` bên trong `select`.

Ví dụ:
- Trong `$scope`:
```
function myController($scope) {
    $scope.ds_chuyen_nganh = [
        { code: "UDPM", text: "Ứng dụng phần mềm" },
        { code: "TKTW", text: "Thiết kế trang web" },
        { code: "LTMT", text: "Lập trình máy tính" },
        { code: "TKDH", text: "Thiết kế đồ họa" },
    ];

    $scope.sv = {
        ...
        chuyen_nganh: ''
    };
}
```

- Sử dụng `ng-repeat` để đổ dữ liệu:
```
<select ng-model="sv.chuyen_nganh">
    <option ng-repeat="nganh in ds_chuyen_nganh">
        {{ nganh.text }}
    </option>
</select>
```

- Sử dụng `ng-options` để đổ dữ liệu:
```
<select
    ng-model="sv.chuyen_nganh"
    ng-options="nganh.text for nganh in ds_chuyen_nganh track by nganh.code">
</select>
```
- Tham khảo: https://docs.angularjs.org/api/ng/directive/ngOptions

- **Lưu ý**:
    - Khi sử dụng `ng-repeat`, thuộc tính `value` ***LUÔN LUÔN*** là **text**.
    - Nếu muốn set `value` của thẻ `option` là các thuộc tính của 1 object, dùng `ng-options`.

## 2. Validation
### 2.1. Validate cơ bản trong AngularJs
### 2.2. Các trạng thái của lỗi
### 2.3. Tùy biến (Customize) Validaion trong AngularJs
