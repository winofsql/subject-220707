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


### jQuery でコンボボックスを作成( PHP と連携 )
```javascript
<script>
// ******************************
// jQuery onload イベント
// ******************************
var syozoku = <?= $json ?>;

var cur_syozoku = "<?= $_POST["syozoku"] ?>";

$(function(){

    // 第一画面の初期フォーカス
    $("#scode").focus();

    // 第二画面の初期フォーカス
    if ( <?= $gno ?> == 2 ) {
        $("#sname")
            .focus()
            .select();

        $.each( syozoku, function( index ){

            if ( cur_syozoku == syozoku[index]["コード"] ) {
                $("#syozoku").append( 
                $('<option>')
                    .text( syozoku[index]["名称"] )
                    .val( syozoku[index]["コード"] )
                    .prop("selected", true )
                );
            }
            else {
                $("#syozoku").append( 
                $('<option>')
                    .text( syozoku[index]["名称"] )
                    .val( syozoku[index]["コード"] )
                );
            }

        });
    }

});
```


### [JavaScript : 文字列処理( メソッド )](http://cya.sakura.ne.jp/js/string.htm)
```
indexOf
文字列を前方検索します。
length
文字列の長さを取得します。
replace
文字列を置換します。
slice
文字列を切り取ります。整数のゼロ埋め(0パディング)。
split
文字列をセパレータで分解します。文字列内に指定文字がいくつあるか。
substr
文字列を切り取ります。
toLowerCase
文字列を小文字に変換します。
toUpperCase
文字列を大文字に変換します。
trim
文字列の両端の空白を削除します。
```
