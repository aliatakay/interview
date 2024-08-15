
# Git Soruları



Git, 3 adet çalışma ağacına sahiptir.

- Working Directory
- Staging Area / Index
- Repository
- Remote Repository ( 3 ağacın sonunda GitHub gibi remote repository'ye pushlanır.)



### Git Komutları

<table>
  <tr>
    <th>Komut</th>
    <th>Açıklama</th>
  </tr>
  <tr>
    <td>git clone</td>
    <td>Remote bir repoyu, local bilgisayara klonlar.</td>
  </tr>
  <tr>
    <td>git status</td>
    <td>Bulunduğumuz branch'i ve working directory'deki değişiklikleri gösterir.</td>
  </tr>
  <tr>
    <td>git add</td>
    <td>Untracked (izlenmeyen) bir dosyayı, git'in takip etmesini sağlar. Aynı zamanda bu komut ile dosyalar, Staging Area'ya taşınmış olur.</td>
  </tr>
  <tr>
    <td>git commit</td>
    <td>Stage'deki dosyaları repository'ye taşır. Tüm dosyalar hala local repo'da bulunmaktadır.</td>
  </tr>
  <tr>
    <td>git push</td>
    <td>Repo'daki dosyaları, github veya benzeri remote repo'ya gönderir.</td>
  </tr>
</table>

---
