# heroku-bash-schedule-example
This is a quick example of how to create a heroku app that just exists to run a bash script on a regular basis.

Heroku's documentation can make you overthink things some times.  You basically just need to get heroku to allocation _some_ sort of dyno that you can then run any command within on a scheduled basis

### Get a copy of this repo, and add heroku target

```
# clone this repo:
git clone git@github.com:ledjon/heroku-bash-schedule-example.git 

# make heroku app (you will need to select another name, probably):
heroku apps:create -n my-heroku-bash-schedule-example

# add heroku as target of a git push (of this repo):
heroku git:remote -a my-heroku-bash-schedule-example

# set the heroku build pack:
heroku buildpacks:set heroku/python
git push heroku master

# start a heroku dyno bash session to test it:
heroku run bash

# you are no in a heroku dyno... test your bash script:
bash /app/runme.sh

exit;
```

### Create the addon and schedule task

These steps can be done from the heroku console, of course:

```
heroku addons:create scheduler:standard
heroku addons:open scheduler 
```

In the scheduler config, put `bash /app/runme.sh` as the command to run.

That should be it!
