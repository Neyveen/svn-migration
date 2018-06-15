### Get repository users
`svn log svn://your-svn-repository --xml | grep -P "^<author" | sort -u | perl -pe 's/<author>(.*?)<\/author>/$1 = NomEspacePrenom <email@yourcompany.com>/' > C:\users.txt`
### Create local git repository
`git svn clone svn://your-svn-repository C:\your\.git\path --authors-file=C:\users.txt --no-metadata -s your-repository-name`
### Transform svn tag to git tags
`git for-each-ref refs/remotes/origin/tags | cut -d / -f 5- | grep -v "@" | Where-Object { git tag "$_" "origin/tags/$_"; git branch -r -d "origin/tags/$_";}`
### Transform svn branches to git branches
`git for-each-ref refs/remotes/origin | cut -d / -f 4- | grep -v "@" | Where-Object { If ($_ -like "trunk") { git branch -r -d "origin/$_";} Else {git branch "$_" "refs/remotes/origin/$_"; git branch -r -d "origin/$_";} }`
### Push
- Remove .git\refs\remotes
- Remove unwanted branches in .git\refs\heads if so
- Remove unwanted tags in .git\ref\tags if so
- Add remote repository `git remote add origin https:\\repoGit.git`
- Execute git push origin --mirror
