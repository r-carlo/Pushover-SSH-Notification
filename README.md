# Pushover-SSH-Notification

#!/bin/bash

# Change these variables
API_TOKEN=""
API_USER=""

if [ "$PAM_TYPE" != "close_session" ]; then
  TITLE="SSH Login: ${PAM_USER}@$(hostname -f) (${PAM_RHOST})"
  TEXT="$(date)"

  curl -s \
  -F "token=$API_TOKEN" \
  -F "user=$API_USER" \
  -F "title=$TITLE" \
  -F "message=$TEXT" \
  -F "priority=0" \
  https://api.pushover.net/1/messages.json >/dev/null 2>&1 &
fi
if [ "$PAM_TYPE" = "close_session" ]; then
  TITLE="SSH Logout: ${PAM_USER}@$(hostname -f) (${PAM_RHOST})"
  TEXT="$(date)"

  curl -s \
  -F "token=$API_TOKEN" \
  -F "user=$API_USER" \
  -F "title=$TITLE" \
  -F "message=$TEXT" \
  -F "priority=0" \
  https://api.pushover.net/1/messages.json >/dev/null 2>&1 &
fi
