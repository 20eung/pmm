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
services:
  kometa:
    image: kometateam/kometa
    container_name: pmm
    hostname: pmm
    restart: unless-stopped
    stdin_open: true
    tty: true
    environment:
      - TZ=Asia/Seoul
      - KOMETA_RUN=true
      - KOMETA_DEBUG=true
      - KOMETA_LOG_REQUESTS=true
      - KOMETA_CONFIG=/config/config.yml
      - KOMETA_OVERLAYS_ONLY=true
      - KOMETA_RUN=true
    volumes:
      - ./config:/config
```


# config.yml

> 설명:

- config 예제 : [https://metamanager.wiki/en/latest/defaults/guide.html](https://metamanager.wiki/en/latest/defaults/guide/)

- 1.1 영화(최근추가) : Plex에서 생성한 라이브러리명과 동일하게 사용합니다. 띄어쓰기까지 동일하게

- plex url/token : Plex 서버를 웹으로 접속한 후 확인할 수 있습니다.

  - 영상을 선택한 후 --> ... 눌러 미디어 정보를 클릭한 후 --> XML 보기를 누르면 새 창이 나옵니다.

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
#   schedule_overlays: weekly(sunday)
    overlay_files:
      - remove_overlays: false
      - reapply_overlay: true
      - default: commonsense
      - default: resolution
        template_variables:
          use_dvhdrplus: false
          use_dvhdr: false
          use_plus: false
          use_dv: false
          use_hdr: false
          use_576p: false
          use_480p: false
      - default: ribbon
      - default: streaming
      - default: ratings
        template_variables:
          rating1: user
          rating1_image: rt_tomato
          rating2: critic
          rating2_image: imdb
          rating3: audience
          rating3_image: tmdb
          horizontal_position: right

  1.2 영화(외국):
#   schedule_overlays: weekly(sunday)
    overlay_files:
      - remove_overlays: false
      - reapply_overlay: true
      - default: commonsense
      - default: resolution
        template_variables:
          use_dvhdrplus: false
          use_dvhdr: false
          use_plus: false
          use_dv: false
          use_hdr: false
          use_576p: false
          use_480p: false
      - default: ribbon
      - default: streaming
      - default: ratings
        template_variables:
          rating1: user
          rating1_image: rt_tomato
          rating2: critic
          rating2_image: imdb
          rating3: audience
          rating3_image: tmdb
          horizontal_position: right


  1.3 영화(한국):
#   schedule_overlays: weekly(sunday)
    overlay_files:
      - remove_overlays: false
      - reapply_overlay: true
      - default: commonsense
      - default: resolution
        template_variables:
          use_dvhdrplus: false
          use_dvhdr: false
          use_plus: false
          use_dv: false
          use_hdr: false
          use_576p: false
          use_480p: false
      - default: ribbon
      - default: streaming
      - default: ratings
        template_variables:
          rating1: user
          rating1_image: rt_tomato
          rating2: critic
          rating2_image: imdb
          rating3: audience
          rating3_image: tmdb
          horizontal_position: right


  operations:
    mass_user_rating_update: mdb_tomatoes
    mass_critic_rating_update: imdb
    mass_audience_rating_update: tmdb
    mass_genre_update: tmdb
    mass_content_rating_update: mdb_commonsense
    mass_originally_available_update: tmdb
    mass_imdb_parental_labels: without_none
        
settings:
  run_order:
  - operations
  - overlays
  - metadata
  - collections

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
  overlay_artwork_filetype: jpg
  overlay_artwork_quality: 100
  playlist_exclude_users:
  playlist_report: false                # false or true
  playlist_sync_to_user: all            # all, list of users, or comma-separated string of users
  prioritize_assets: false              # false or true
  run_again_delay: 0                    # 0 or any integer
  save_report: false                    # false or true
  show_asset_not_needed: false          # true or false
  show_filtered: false                  # false or true
  show_missing: false                   # true or false
  show_missing_assets: false            # true or false
  show_missing_episode_assets: false    # false or true
  show_missing_season_assets: false     # false or true
  show_options: false                   # false or true
  show_unconfigured: true               # false or true
  show_unmanaged: false                 # true or false
  sync_mode: append                     # append or sync
  tvdb_language: kor                    # Any ISO 639-2 Language Code
  verify_ssl: true                      # true or false


## Required
plex:
  url: https://34-64-~~~.plex.direct:32400
  token: Ek4PJGxH~~~
  timeout: 60                           # 60 or any integer
  db_cache:
  clean_bundles: false                  # false or true
  empty_trash: false                    # false or true
  optimize: false                       # false or true
  verify_ssl:

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
    # everything below is autofilled by the script
    access_token:
    token_type:
    expires_in:
    refresh_token:
    scope:
    created_at:

```

# pmm-run.sh

pmm 은 지정된 시간에 매일같이 라이브러리 정보를 업데이트합니다.

수동으로 업데이트하기 위한 스크립트입니다.

```
#!/bin/sh

docker run --rm -it -v "./config:/config:rw" kometateam/kometa --config /config/config.yml --ignore-schedules --run
```
