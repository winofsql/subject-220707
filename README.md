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
    - アンカーでキャンボタン
    ```html
    <a href="http://localhost/php-0707-01/php-mtn-v04-communication/syain.php" class="btn btn-primary ms-4">キャンセル</a>
    ```
    - アンカーに PHP 変数埋め込み
    ```
    <a href="<?= $_SERVER["PHP_SELF"] ?>" class="btn btn-primary ms-4">キャンセル</a>
    ```
    - PHP 側の値を JavaScript で使用する
    ```javascript
    // <?= $_SERVER["SCRIPT_NAME"] ?>
    // <?= $_SERVER["PHP_SELF"] ?>

    var self = "<?= $_SERVER["PHP_SELF"] ?>";

    $(function(){
        $("#cancel").on("click", function(){
            start_page();
            // document.location.href="http://localhost/php-0707-01/php-mtn-v04-communication/syain.php";
        });
    });

    function start_page() {
        document.location.href = self;
    }
    ```
    - jQuery で 次の入力フィールドを探す( **php-mtn-v05-enter-control** )\
    ![image](https://user-images.githubusercontent.com/1501327/177698426-08d7d76d-1db5-41f8-87da-a66fb8c75203.png)
