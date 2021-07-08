# yushitianx
php+html+css

詳情頁代码
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>商品详情页</title>
<link href="css/zz.css" rel="stylesheet" type="text/css">
</head>
<body>
<div class="top">
    <?php include("top.php");?>
</div>
<div class="one">
  <div class="DT">
      <?php
      session_start();
      include("conn/conn.php");
      $id=$_REQUEST["id"];
      $sqlstr="select tupian from tb_shangpin where id=$id";
      $result = mysqli_query($conn,$sqlstr);
      $row = mysqli_fetch_row($result);
      echo "<img class='image' src='".$row[0]."' />";
      ?>
  </div>
  <div class="xx">
    <p class="onep">
        <?php
        $id=$_REQUEST["id"];
        $sqlstr="select mingcheng from tb_shangpin where id=.$id";
        $result = mysqli_query($conn,$sqlstr);
        $rows = mysqli_fetch_row($result);
        echo $rows[0];
        ?>
    </p>
    <P class="onep1">
        <?php
        $id=$_REQUEST["id"];
        $sqlstr="select price,vipprice from tb_shangpin where id=$id";
        $result = mysqli_query($conn,$sqlstr);
        $row = mysqli_fetch_row($result);
        echo "￥".$row[0];
        ?>
    </p>
    <p class="onep3">
        <?php echo "会员价：￥".$row[1]; ?>
    </p>
    <P class="onep2">商品库存数量:
        <?php
        $id=$_REQUEST["id"];
        $sqlstr="select shuliang from tb_shangpin where id=$id";
        $result = mysqli_query($conn,$sqlstr);
        $rows1 = mysqli_fetch_row($result);
        echo $rows1[0];
        ?>
    </P>
    <form method="POST" action="shopping.php?id=<?php echo $_REQUEST["id"];?>&price=<?php echo $row[0];?>&vipprice=<?php echo $row[1];?>&spname=<?php echo $rows[0];?>">
        <input type="number" name="num" step="1" min="1" max="5" value="1"/>
        <input type="submit" id="buy" value="购买">
    </form>
  </div>
</div>
<?php
//if(isset($_SESSION['username']) && $_SESSION['username']!="")
//{
?>
<form method="POST" action="pj.php?id=<?php echo $_REQUEST["id"];?>">
  <div class="end">
        <p class="onep">商品评价：</p>
            <textarea class="text" name="text" placeholder="请发表您的评价"></textarea>
            <input type="submit" id="submit" name="submit" value="提交">
  </div>
  <div class="pj" >
     <table class="table">
     <?php
         $sql=mysqli_query($conn,"select count(*) as total from tb_pingjia where spid=$id");
         $info=mysqli_fetch_array($sql);
         $total=$info['total'];
         if($total==0) {
             echo "本商品暂无评论信息!";
         }
         else{?>
         <tr>
             <td class="table1">用户名</td>
             <td class="table2">商品名</td>
             <td class="table3">评论内容</td>
             <td class="table4">评论时间</td>
         </tr>
     <?php
         $sql1=mysqli_query($conn,"select * from tb_pingjia where spid=$id order by time desc");
         while($info1=mysqli_fetch_array($sql1)) {
     ?>
     <tr>
         <td class="table1">
             <?php
             $spid=$info1['userid'];
             $sql3=mysqli_query($conn,"select name from tb_user where id=$spid");
             $info3=mysqli_fetch_array($sql3);
             echo $info3['name'];
             ?>
         </td>
         <td class="table2">
             <?php
             $spid=$info1['spid'];
             $sql2=mysqli_query($conn,"select mingcheng from tb_shangpin where id=$spid");
             $info2=mysqli_fetch_array($sql2);
             echo $info2['mingcheng'];
             ?>
         </td>
         <td class="table3">
             <?php echo $info1['content']; ?>
         </td>
         <td class="table4">
             <?php echo $info1['time']; ?>
         </td>
     </tr>
     <?php } } ?>
     </table>
  </div>
</form>
<?php
//}
?>
<footer >
    <img src="images/DT9.jpg" width="1180px" class="two2"/>
  <div class="bottom">
    <?php include("bottom.php");?>
  </div>
</footer>
</body>
</html>
