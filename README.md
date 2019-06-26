# Killport command
A easy command to kill services running on your lovely port.
```
This is intended to work on unix systems, particularly MacOS.
```

-----
## Example

![example](https://github.com/AlberErre/kill-port-command/blob/master/example.png)

-----

## Instructions:

#### 1. navigate to `/usr/local/bin/` folder.
#### 2. create a file named `killport`. 
```
touch killport
```
#### 3. paste the code below on that file:
```
#!/bin/bash
touch temp.text
lsof -n -i4TCP:$1 | awk '{print $2}' > temp.text
pidToStop=`(sed '2q;d' temp.text)`
> temp.text
if [[ -n $pidToStop ]]
then
kill -9 $pidToStop
echo "Done. Service running on port $1 has stopped."
else
echo "Sorry, there is nothing running on port $1"
fi
rm temp.text
```
#### 4. set permission to the file.
```
chmod 755 killport
```
#### 5. Done, kill any process on your selected port, e.g. port 3000:
```
killport 3000
```
