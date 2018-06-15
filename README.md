### Get repository users
`svn log svn://your-svn-repository --xml | grep -P "^<author" | sort -u | perl -pe 's/<author>(.*?)<\/author>/$1 = NomEspacePrenom <email@yourcompany.com>/' > C:\users.txt`
### Create local git repository
`git svn clone svn://your-svn-repository C:\your\.git\path --authors-file=C:\users.txt --no-metadata -s your-repository-name`
### Transform remote tag in git tags
`git for-each-ref refs/remotes/origin/tags | cut -d / -f 5- | grep -v "@" | Where-Object { git tag "$_" "origin/tags/$_"; git branch -r -d "origin/tags/$_";}`
### Transform branches in git branches
`git for-each-ref refs/remotes | cut -d / -f 3- | grep -v "@" | Where-Object { git branch "refs/remotes/$_"; git branch -r -d "$_"; }`
