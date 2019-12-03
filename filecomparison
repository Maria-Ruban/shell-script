#!/bin/bash

#### Assign variable for md5sum storing files
prodlist="/home/ruban/md5test/md5listmark_prod"    #mention your local machine path to store the md5sum values
stagelist="/home/ruban/md5test/md5listmark_stage"  #mention your local machine path to store the md5sum values



## Generate two output files
md5sum /home/ruban/md5test/prod/* > $prodlist
md5sum /home/ruban/md5test/stage/* > $stagelist

## Replace the folder name by * symbol
sed -i 's/prod/*/g' $prodlist
sed -i 's/stage/*/g' $stagelist

## find the difference between the files
echo -en '\n'
echo -e  "\e[38:2::240:143:104mFind the difference between Prod and Staging environment by status of the color.
If there are no color changes on both side(looks white), Prod and Staging environments are up to date. \e[0m"

echo -e " \e[1m                        Production                                            QA\e[0m"
colordiff -y <(awk '{print $1$2}' $prodlist) <(awk '{print $1$2}' $stagelist)

echo -en '\n'

## Update the result of md5sum status
if diff -y <(awk '{print $1}' $prodlist) <(awk '{print $1}' $stagelist) > /dev/null
then
        echo -e  "\e[4mStatus of md5sum\e[0m"
        echo -e "\e[38:5:42mmd5sum matching in both Prod and staging env\e[0m"

else
        echo -e  "\e[4mStatus of md5sum\e[0m"        
        echo -e "\e[31mmd5sum not matching\e[0m"

fi
