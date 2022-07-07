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
