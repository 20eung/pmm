# pmm-config
Plex Meta Manager Configuration

# Tree

```
/data/pmm/
├── config
│   ├── UUID
│   ├── assets
│   ├── config.yml
│   ├── config.movie.foreign.yml
│   ├── config.movie.kor.yml
│   ├── config.movie.new-clear.yml
│   ├── config.movie.new.yml
│   ├── logs
│   └── overlays
├── docker-compose.yml
├── pmm-run-movie-foreign.sh
├── pmm-run-movie-kor.sh
├── pmm-run-movie-new-clear.sh
├── pmm-run-movie-new.sh
└── pmm-run.sh
```

# docker-compose.yml

```
version: "2.1"
services:
  plex-meta-manager:
    image: meisnate12/plex-meta-manager:latest
    container_name: plex-meta-manager
    hostname: pmm
    restart: unless-stopped
    network_mode: host
    environment:
      - TZ=Asia/Seoul
      - PLEX_MEDIA_SERVER_USER=plex
      - PUID=1001
      - PGID=1001
    volumes:
      - /etc/timezone:/etc/timezone
      - ./config:/config
```

PUID, PGID는 Plex Meta Manager를 실행할 User ID를 사용합니다.

리눅스 쉘에서 id 입력하면 uid와 gid를 알아낼 수 있습니다.

```
ubuntu@:/data$ id
uid=1001(ubuntu) gid=1001(ubuntu) 
groups=1001(ubuntu),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),
44(video),46(plugdev),119(netdev),120(lxd),999(docker)
```

# config.yml

> 설명:

- config 예제 : https://metamanager.wiki/en/latest/defaults/guide.html

- 1.1 영화(최근추가) : Plex에서 생성한 라이브러리명과 동일하게 사용합니다. 띄어쓰기까지 동일하게

- plex url/token : Plex 서버를 웹으로 접속한 후 확인할 수 있습니다.

  - 영상을 선택한 후 ... 눌러 미디어 정보를 클릭한 후 XML 보기를 누르면 새 창이 나옵니다.

  - 앞 부분이 URL이고, 마지막 부분이 Token 입니다.

<img src=./images/xml.png>

<img src=./images/url.png>

<img src=./images/token.png>


- tmdb apikey : tmdb 회원 가입 후 생성할 수 있습니다.
- mdblist apikey : mdblist 회원 가입 후 생성할 수 있습니다.
- trakt client_id/client_secret/pin : trakt 회원 가입 후 생성할 수 있습니다.


```
## This file is a template remove the .template to use the file

## Required
libraries:
  1.1 영화(최근추가):
    overlay_path:
    - remove_overlays: false
    - reapply_overlay: true
    - pmm: commonsense
    - pmm: resolution
    - pmm: ribbon
    - pmm: streaming
    - pmm: ratings
      template_variables:
        horizontal_position: right
        rating1: critic
        rating1_image: imdb
        rating2: audience
        rating2_image: tmdb

    settings:
      asset_directory:
      - config/assets

    operations:
      mass_critic_rating_update: imdb
      mass_audience_rating_update: tmdb
      mass_genre_update: tmdb
      mass_content_rating_update: mdb_commonsense
      mass_originally_available_update: tmdb
      mass_imdb_parental_labels: without_none

      
  1.2 영화(외국):
    overlay_path:
    - remove_overlays: false
    - reapply_overlay: true
    - pmm: commonsense
    - pmm: resolution
    - pmm: ribbon
    - pmm: streaming
    - pmm: ratings
      template_variables:
        horizontal_position: right
        rating1: critic
        rating1_image: imdb
        rating2: audience
        rating2_image: tmdb

    settings:
      asset_directory:
      - config/assets

    operations:
      mass_critic_rating_update: imdb
      mass_audience_rating_update: tmdb
      mass_genre_update: tmdb
      mass_content_rating_update: mdb_commonsense
      mass_originally_available_update: tmdb
      mass_imdb_parental_labels: without_none

  1.3 영화(한국):
    overlay_path:
    - remove_overlays: false
    - reapply_overlay: true
    - pmm: commonsense
    - pmm: resolution
    - pmm: ribbon
    - pmm: streaming
    - pmm: ratings
      template_variables:
        horizontal_position: right
        rating1: critic
        rating1_image: imdb
        rating2: audience
        rating2_image: tmdb

    settings:
      asset_directory:
      - config/assets

    operations:
      mass_critic_rating_update: imdb
      mass_audience_rating_update: tmdb
      mass_genre_update: tmdb
      mass_content_rating_update: mdb_commonsense
      mass_originally_available_update: tmdb
      mass_imdb_parental_labels: without_none

settings:
  asset_depth: 0                        # 0 or any integer
  asset_directory:                      # any directory
  asset_folders: true                   # true or false
  cache: true                           # true or false
  cache_expiration: 60                  # 60 or any integer
  check_nightly: true                   # true or false
  create_asset_folders: false           # false or true
  custom_repo:                          # link to base repository
  default_collection_order: release     # release or alpha or custom
  delete_below_minimum: false           # false or true
  delete_not_scheduled: false           # false or true
  dimensional_asset_rename: false       # false or true
  download_url_assets: false            # false or true
  ignore_ids:                           # List or comma-separated string of TMDb/TVDb IDs
  ignore_imdb_ids:                      # List or comma-separated string of IMDb IDs
  item_refresh_delay: 0                 # 0 or any integer
  minimum_items: 1                      # 1 or any integer
  missing_only_released: false          # false or true
  only_filter_missing: false            # false or true
  playlist_exclude_users:
  playlist_report: false                # false or true
  playlist_sync_to_user: all            # all, list of users, or comma-separated string of users
  prioritize_assets: false              # false or true
  run_again_delay: 0                    # 0 or any integer
  show_asset_not_needed: false          # true or false
  show_filtered: false                  # false or true
  show_missing: false                   # true or false
  show_missing_assets: false            # true or false
  show_missing_episode_assets: false    # false or true
  show_missing_season_assets: false     # false or true
  sync_mode: append                     # append or sync
  show_options: false                   # false or true
  save_report: false                    # false or true
  show_unconfigured: true               # false or true
  show_unmanaged: false                 # true or false
  tvdb_language: kor                    # Any ISO 639-2 Language Code
  verify_ssl: true                      # true or false


## Required
plex:
  url: https://34-64-~~~.plex.direct:32400
  token: Ek4PJGxH~~~
  timeout: 60                           # 60 or any integer
  clean_bundles: false                  # false or true
  empty_trash: false                    # false or true
  optimize: false                       # false or true
  db_cache:


tmdb:                                   # REQUIRED for the script to run
  apikey: 9cea8d49d95~~~
  language: ko                          # ISO 639-1 Code of the User Language
  region: KR                            # ISO 3166-1 Code of the User Region for Searches
  cache_expiration: 60                  # Number of days


mdblist:
  apikey: cr8rn5~~~
  cache_expiration: 60

trakt:
  client_id: 3d8bc~~~~
  client_secret: 268f~~~~
  pin: 318F~~~~
  authorization:
    access_token:
    token_type:
    expires_in:
    refresh_token:
    scope:
    created_at:

```

# pmm-run.sh

pmm 은 지정된 시간에 매일같이 라이브러리 정보를 업데이트합니다.

수동으로 하기 위한 스크립트입니다.

```
#!/bin/sh

docker run --rm -it -v "./config:/config:rw" meisnate12/plex-meta-manager --config /config/config.yml --ignore-schedules --run
```
