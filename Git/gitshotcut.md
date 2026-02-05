## git change a contributor on its 
git checkout --orphan clean-main
git add .
git commit -m "Initial commit"
git branch -D main
git branch -m main
git push -f origin main
git log --oneline --all
git push --force --all
git push --force --tags
# empty commit to force recalculation
git commit --allow-empty -m "Trigger contributor recalculation"
git push -f origin main
