
# Git Soruları



Git, 3 adet çalışma ağacına sahiptir.

- Working Directory
- Staging Area / Index
- Repository
- Remote Repository ( 3 ağacın sonunda GitHub gibi remote repository'ye pushlanır.)



### Git Komutları



**git clone <*url*>** 					Remote bir repoyu, local bilgisayara klonlamak için

**git status** 			 				Bulunduğumuz branch'i görmek için

​                              				Working Tree'deki değişiklikleri görmek için

**git add <*filename*>** 	 		Untracked (izlenmeyen) bir dosyayı, git'in takip etmesini sağlar.

​											  Aynı zamanda bu komut ile dosyalar, Staging Area'ya taşınmış olur.

**git commit -m <*mesaj*>** 	  Stage'deki dosyaları repository'ye taşır.

​											   Tüm dosyalar hala local repo'da bulunmaktadır.

**git push origin master** 		Repo'daki dosyaları, remote repo'ya gönderir. (GitHub gibi)



---
