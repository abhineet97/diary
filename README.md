diary
=====
>Keep a diary.

Simple bash script that helps you keep a virtual text-only diary.

Don't worry about anybody else reading your diary because diary.sh encrypts all entries.

Usage
-----
First of all you might wanna set some configs in the `.diaryrc` file like for example the editor to use to write entries in (default is vim)

After that simply invoke diary to create a new entry and then go ahead and type your first diary entry.

```sh
./diary
```
For decrypting the entries do:
```sh
./diary -d
```
For encrypting the entries do:
```sh
./diary -e
```

About The Encryption
-------------------
diary uses GPG with `-c` (symmetric) switch to encrypt a gziped tar file containing all the diary entries.

License
-------
[MIT](LICENSE.txt)
