รายชื่อกลุ่ม 

1.Sirimongkol Wongfu

2.Pattama Thongprapai

3.Ardnarong Boonkerd

=========================

เข้าหน้า bWAPP - XSS Reflected (User-agent)
![GitHub_Logo](/Pic/x1.2.jpg)

จากนั้นทำการ Scan หาช่องโหว่ โดย Rips พบว่า code มีช่องโหว่ของ XSS ที่ส่วนของ User-agent
![GitHub_Logo](/Pic/x1.9.jpg)

ทำการทดสอบด้วยโปรแกรม Brup Suite โดยการแก้ไข User-Agent เป็น <script>alert("XSS")</script>
![GitHub_Logo](/Pic/x1.4.jpg)

พบว่าระบบสามารถโจมตีด้วย XSS ได้
![GitHub_Logo](/Pic/x1.5.jpg)

ทำการตรวจสอบโค้ด
<div id="main">
    <h1>XSS - Reflected (User-Agent)</h1>
    <?php
    if(isset($_SERVER["HTTP_USER_AGENT"]))
    {
        // print_r($_SERVER);
        $user_agent = $_SERVER["HTTP_USER_AGENT"]; >> จุดที่ต้องทำการแก้ไข
        echo "<p>Your User-Agent: <i>" . xss($user_agent) . "</i></p>";
    }
    else
    {
        echo "<p><font color=\"red\">No User-Agent was used!</font></p>";
    }
    ?>
</div>

ทำการแก้ไขโดยวิธีการเพิ่ม strip_tags ไว้หน้าตัวแปร
![GitHub_Logo](/Pic/x1.8.jpg)

ซึ่งจะพบว่าหากทำการสแกนด้วย Rips จะเห็นว่ายังไม่เพียงพอต่อการป้องกัน โดยระบบจะแนะนำให้ใช้  htmlentities
![GitHub_Logo](/Pic/x1.11.jpg)

และหากแก้ไขเป็น htmlentities หากทำการสแกนด้วย Rips จะพบว่าส่วนนั้นได้หายไป
![GitHub_Logo](/Pic/x1.1.jpg)

จากนั้นทำการทดสอบช่องโหว่อีกครั้ง จะพบว่าช่องโหว่ได้รับการแก้ไข
![GitHub_Logo](/Pic/x1.5.jpg)


