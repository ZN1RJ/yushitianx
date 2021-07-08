# yushitianx
php+html+css
<?php
session_start();
include("conn/conn.php");
$content=$_POST['text'];
if($content==""){
    echo "<script>alert('评论不能为空!');
    window.history.back(-1);
    </script>";}
else{
$time=date("Y-m-d H:i:s");
$spid=$_REQUEST["id"];
//$sql=mysqli_query($conn,"select * from tb_user where name='".$_SESSION['username']."'");
//$info=mysqli_fetch_array($sql);
//$userid=$info['name'];
$sql = "insert into tb_pingjia(userid,spid,content,time) values ('123','$spid','$content','$time')";
if(mysqli_query($conn,$sql)){
    echo "<script>alert('评论发表成功!');
     window.history.back(-1);
    </script>";
}
else{
    echo "<script>alert('评论发表失败!');
    window.history.back(-1);
    </script>";
}}
