# salstack
creating salt-master and minions with docker 


You need to just run following commmand to start salt-master in foreground: 
docker-compose up 

In order to start containers in background:
docker-compose up -d

This will start one salt-master instance and two minion instances with aliases salt-master,salt-minion-1,salt-minion-2 respectively.

If you see minions are not connected with master still after all instances are up,this may be due to keys are not automatically accepted by master.
Run following command in another terminal:

docker-compose exec salt-master salt-key -A -y salt-minion


Setup is all ready and we can test with simple ping command.

Login to another salt-master terminal with following command: 
docker-compose exec salt-master sh

Once in, run following ping command for testing:

salt '*' test.ping

and in the window where you started docker compose, you will see the log output of both the master sending the command and the minion receiving the command and replying.

The Salt Remote Execution Tutorial - https://docs.saltstack.com/en/latest/topics/tutorials/modules.html has some quick examples of the comamnds you can run from the master.

Note: you will see log messages like : "Could not determine init system from command line" - those are just because salt is running in the foreground and not from an auto-startu
