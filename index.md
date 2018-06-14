# Get repository users
svn log svn://your-svn-repository --xml | grep -P "^<author" | sort -u | perl -pe 's/<author>(.*?)<\/author>/$1 = /' > C:\users.txt
# Create local git repository
git svn clonesvn://your-svn-repository C:your\.git\path --authors-file=C:\users.txt --no-metadata -s your-repository-name
# Transform remote tag in git tags
git for-each-ref refs/remotes/tags | cut -d / -f 4- | grep -v "@" | Where-Object { git tag "$_" "tags/$_"; git branch -r -d "tags/$_";}
# Transform branch tag in git branches
git for-each-ref refs/remotes | cut -d / -f 3- | grep -v "@" | Where-Object { git branch "refs/remotes/$_"; git branch -r -d "$_"; }
