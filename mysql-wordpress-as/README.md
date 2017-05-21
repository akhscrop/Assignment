Installing WordPress with auto scaling

Put your desired MySQL password in a file called password.txt with no trailing newline. The first tr command will remove the newline if your editor added one.

Note: if your cluster enforces selinux and you will be using Host Path for storage, then please follow this extra step.

tr --delete '\n' <password.txt >.strippedpassword.txt && mv .strippedpassword.txt password.txt

kubectl create -f https://raw.githubusercontent.com/akhscrop/Assignment/master/mysql-wordpress-as/local-volumes.yaml

kubectl create secret generic mysql-pass --from-file=password.txt

kubectl create -f https://raw.githubusercontent.com/akhscrop/Assignment/master/mysql-wordpress-as/mysql-deployment.yaml

kubectl create -f https://raw.githubusercontent.com/akhscrop/Assignment/master/mysql-wordpress-as/wordpress-deployment.yaml

kubectl autoscale deployment wordpress --cpu-percent=50 --min=1 --max=10
