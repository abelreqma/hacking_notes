**WordPress**
```
cat /var/www/html/wp-config.php | grep 'DB_USER\|DB_PASSWORD'
```
**Spool/Mail Directories**
```
find / ! -path "*/proc/*" -iname "*config*" -type f 2>/dev/null
```
**Current User SSH Files**
```
ls ~/.ssh
```
**authorized_key File**
```
find / -name authorized_keys 2> /dev/null
```
**Private Keys**
```
find / -name id_rsa 2> /dev/null      #likely naming convention
```
**"Password" String**
```
#Try variations on the string "password"
find . -type f -exec grep -i -I "PASSWORD" {} /dev/null \;     # Looks for "password" in current directory
grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null      #entire filesystem
grep --color=auto -rnw '/' -ie "PASSWORD=" --color=always 2> /dev/null      #entire filesystem
locate password | more
locate pass | more
```
