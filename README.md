# subject-220707

### window.open で開いたウインドウにアクセスする
```javascript
var url = "http://localhost/php-0706-01/php-req-v01-basic/syain.php";
var winname = "new_windpow";
var option = "width=800,height=500,left=800,top=100";
var handle;

$( function(){

    $("#open").on("click", function(){
        handle = window.open(url, winname, option);
    });

});
```

### opener が存在しない場合の対処
```javascript
    $("tr").on("click", function(){
        var scode = $(this).find("td").eq(0).text();
        if ( opener != null ) {
            opener.$("#scode").val(scode);
            opener.$("#btn").click();
            window.close();
        }
    });
```

- ### キャンセルボタン(処理含む)のバリエーション
    - jQuery の処理
    ```javascript
    $(function(){
        $("#cancel").on("click", function(){
            document.location.href="http://localhost/php-0707-01/php-mtn-v04-communication/syain.php";
        });
    });
    <input <?= $disabled_2 ?> type="button" name="cancel" id="cancel" class="btn btn-primary ms-4" value="キャンセル">
    ```
    - function を HTML 内から呼ぶ
    ```
    function start_page() {
        document.location.href="http://localhost/php-0707-01/php-mtn-v04-communication/syain.php";
    }
    <input
        <?= $disabled_2 ?>
        type="button"
        name="cancel"
        class="btn btn-primary ms-4" 
        value="キャンセル" 
        onclick='start_page();';
    >
    ```
