# -BASH-SCRIPT-FOR-PRINT-ELF-FILE-IN-ACENTING-ORDER
cd $1
x=0
for i in *
do
 if [ -x $i ]
  then
  file[ x++]=$i
 fi
done
echo ${file[@]}


for (( i=0;i<${#file[@]};i++ ))
do
l=$( stat -c %s ${file[i]} )
for (( j=i+1;j<${#file[@]};j++ ))
do
k=$( stat -c %s ${file[j]} )
if [ l > k ]
then
temp=${file[i]}
file[i]=${file[j]}
file[j]=$temp
fi                                                    done
done
done

for (( i=0;i<${#file[@]};i++ ))
do
echo ${file[i]}
done
