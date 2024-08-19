**TO-DO** <br>
1- Ansible, Linux'ta çalışan bir otomasyon aracıdır. Bu nedenle bir playbook oluşturup onu çalıştırmak için ssh'a bağlandım. <br> 
2- $ **ssh mina-unal@mina-unal-codecamp24.obss.io -p 8022** <br>
3- Bende pip kurulu olduğundan my-ansible-case-2-repository içerisinde bir "myplaybook" klasörü oluşturdum. sudo yetkisiyle **$ pip install ansible** dedim. Çıkan bütün izinleri onayladım. <br>
4- Daha sonra ansible'ın resmi sitesinden **$ ansible-galaxy role install geerlingguy.docker** indirdim.<br>
5- Bu aşamada **ansible-galaxy init** işlemini yaptım. Böylece içinde readme.md bulunan bir repo oluştu.
6- Bu projede /tests içerisinde bulunan inventory.ini dosyasındaki localhost, playbook'umun sadece local makinalarımda çalışacağını gösterir.<br>
7- Repoda hazır gelen /ports dizininde bir yml dosyası oluşturdum. Bu yml dosyası oluşturacağım makine/makineler için hazır configuration'lar sağlayacak. <br>

Bu dosya 5 alt task'e bölünmüştür. Sırasıyla taskler ve yaptığı işler aşağıda gösterilmiştir.<br>
**TASKS** <br>

**TASK 1** <br>
**name**: Görev, "Create an empty file if it does not exist" (Eğer yoksa boş bir dosya oluştur) olarak adlandırılmıştır. <br>
**ansible.builtin.file**: Bu modül, belirtilen dosya veya dizin üzerinde dosya sistemi işlemleri gerçekleştirir. <br>
**path**: /home/mina-unal/my-ansible-case-2-repository/myplaybook/tasks/deneme.txt dosya yolunu gösterir. <br>

**TASK 2** <br>
**name**: "Add Hello World content to the file" (Dosyaya Hello World içeriği ekle).<br>
**ansible.builtin.copy**: Bu modül, dosya veya dizinleri kopyalamak ve içerik eklemek için kullanılır.<br>
**dest**: Hedef dosya olarak aynı yolu (/home/mina-unal/my-ansible-case-2-repository/myplaybook/tasks/deneme.txt) belirtir.<br>
**content**: Dosyaya eklenecek içerik olarak "Hello, World!\n" metnini içerir.<br>
**mode**: Dosya izinleri 0644 olarak ayarlanır, bu da sahibin okuma ve yazma, grubun ve diğer kullanıcıların sadece okuma yetkisine sahip olmasını sağlar.<br>

**TASK 3** <br>
**name**: "Update the file content" (Dosya içeriğini güncelle).<br>
**ansible.builtin.copy**: Aynı modül kullanılır, ancak bu kez içerik "Today is 30th of the July\n" olarak değiştirilir.<br>
**dest**: aynı dosya yolunu gösterir.<br>
**content**: Bu adım, önceki "Hello, World!" içeriğini "Today is 30th of the July\n" ile değiştirir. copy modülü, belirtilen içeriği dosyanın tamamına yazar, yani önceki içeriği tamamen siler.<br>

**TASK 4**<br>
**name**: "Change permissions of the file to 0755" (Dosya izinlerini 0755 olarak değiştir).<br>
**ansible.builtin.file**: Dosya izinlerini değiştirmek için kullanılır.<br>
**path**: Aynı dosya yolu.<br>
**mode**: Dosya izinleri 0755 olarak ayarlanır. Bu, sahibin okuma, yazma ve çalıştırma; grubun ve diğer kullanıcıların ise okuma ve çalıştırma yetkilerine sahip olacağı anlamına gelir.<br>

**TASK 5**<br>
**name**: "Copy deneme.txt to backup directory" (deneme.txt dosyasını files dizininin içine kopyalayacak).<br>
**ansible.builtin.copy**: Dosyayı kopyalamak için kullanılır.<br>
**src**: Kaynak dosya yolu olarak /home/mina-unal/my-ansible-case-2-repository/myplaybook/tasks/deneme.txt belirtilir.<br>
**dest**: Hedef dizin olarak /home/mina-unal/my-ansible-case-2-repository/myplaybook/files belirtilir. Bu, dosyanın belirtilen hedef dizine kopyalanacağı anlamına gelir.<br>

.yml dosyasını çalıştırmak için kullandığım komut: <br>
**$ ansible-playbook -i inventory.ini playbook.yml**

Bu işlemler sonucunda şu çıktıyı aldım. Fotoğrafta en altta güncel dosya içeriği de görünmektedir.
![Alt text](screenshots/playbook.png) 

Böylece ansible-galaxy ile localimdeki makinaya istediğim işlemleri sırasıyla yaptırabildim.





