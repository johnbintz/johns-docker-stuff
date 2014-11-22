These are two of the services I've converted to Docker images that I run on my
home server. You can run them like so:

    docker run -d -p 3689:3689 -v /media:/yourfiles -e MUSIC_DIR=music \
      -v /var/cache/forked-daapd:/localdb johnbintz/forked-daapd
    docker run -d -p 8200:8200 -p 1900:1900 -v /media:/yourfiles \
      -e MOVIES_DIR=movies -e PODCASTS_DIR=music \
      -v /var/lib/minidlna:/localdb johnbintz/minidlna

Have fun.
