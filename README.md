## Readme Generator

(command-line/website) that analyzes your repo code percentage and adds nice sections such as the correct install instructions to your Readme in a safe manner.

## Current Usage:
```bash
# not currently implemented npx readmegenerator
```

## Plan:

1) get the organization and repo
```bash
url=$(git remote get-url origin) &&
suffix=$(basename $url) &&
organization=$(basename ${url%"$suffix"}) &&
repo=$(basename $url .git) &&
echo $organization $repo || echo 'something failed'
```

2) get the languages for the project:
```
curl https://api.github.com/repos/michaeldimmitt/meetup-subscribe/languages
{
  "JavaScript": 27686,
  "HTML": 1586,
  "CSS": 848
}
curl https://api.github.com/repos/michaeldimmitt/$dir/languages
```
3) Check the Readme to see if it needs install instructions:
```bash
cat R*.md | grep "Setup\|Usage\|Install"
```

4) Calculate the percentages and determine if they are acceptable to add install instructions to the readme.

5) Download the winning Readme files:
```bash
cp R*.md AppendedReadme.md
curl -L https://raw.githubusercontent.com/MichaelDimmitt/readmegenerator/master/readmes/React.md >> AppendedReadme.md
curl -L https://raw.githubusercontent.com/MichaelDimmitt/readmegenerator/master/readmes/javascript.md >> AppendedReadme.md

echo 'Your readme is ready! check using: 
cat AppendedReadme.md; 

or accept the chages using:
mv AppendedReadme.md; Readme.md;

If you do not like the resulting git diff, undo our changes with git checkout Readme.md; 😘'
```

## Alternatives if the Plan goes wrong.
1) get the name of the project:
```bash
dir=${PWD##*/}
echo $dir
```

2) get the remote
```
# url=$(git remote -v | grep fetch | awk '{print $2}')
# $(git config --get remote.origin.url)
# this is not the correct url for api... maybe I will use gh_reveal's url parser to build the url.
```

## Additional Links:
https://github.com/MichaelDimmitt/automate-shared-markdown/blob/master/Readme.md
