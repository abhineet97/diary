#!/bin/bash

configs=./.diaryrc
date_format=+%d-%b-%Y
ext="md"
file="$(date $date_format).$ext"
entries="entries"
editor="vim"

if [[ -d $configs ]]; then
  source "$configs"
fi

function new_entry {
if [[ -f $entries.tar.gz.gpg ]]; then
  decrypt_entries
elif [[ ! -d $entries ]]; then
  echo "Creating a new directory $entries ..."
  mkdir $entries
fi
echo "Creating A New Entry..."
printf "\n#%s\n" "$(date +%H:%M)" >> "$entries/$file"
$editor "$entries/$file"
}

function encrypt_entries {
if [[ -f "$entries.tar.gz.gpg" ]]; then
  echo "$entries.tar.gz.gpg already present."
  return 1
elif [[ ! -d "$entries" ]]; then
  echo "No Entries directory present to encrypt."
  return 1
elif [[ -z $(ls $entries/*.$ext) ]]; then
  echo "No unencrypted file present in entries directory"
  return 1
elif [[ ! -f "$entries.tar.gz" ]]; then
  tar czf $entries.tar.gz $entries
fi
echo "Encrypting Diary Entries..."
gpg -c $entries.tar.gz
if [[ $? = 0 ]]; then
  rm -rf $entries.tar.gz $entries
fi
}

function decrypt_entries {
if [[ -d $entries ]]; then
  echo "A decrypted $entries directory is already present"
  return 0
elif [[ ! -f $entries.tar.gz.gpg ]]; then
  echo "Cannot find $entries.tar.gz.gpg"
  return 1
fi
echo "Decrypting Diary Entries..."
gpg -d $entries.tar.gz.gpg > $entries.tar.gz
if [[ $? = 0 ]]; then
  tar xzf $entries.tar.gz
  rm -rf $entries.tar.gz.gpg $entries.tar.gz
fi
}

if [[ -n $1 ]]; then
  if [[ $1 = "-e" ]]; then
     encrypt_entries
  elif [[ $1 = "-d" ]]; then
     decrypt_entries
   fi
  exit $?
fi

new_entry
encrypt_entries
