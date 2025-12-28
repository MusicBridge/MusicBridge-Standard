# Endpoints for MBs-1.0

## GET /
### Response 200
#### body
- "supported_standard_versions": "LIST_MBs-X.X"
- "provider_idintificator": "SERVICE_NAME"
- "provider_repositore": "LINK_TO_PROVIDER_GITHUB_REPOSITORY"

## GET /search?text=DATA
### Request

#### Query parameters: 
- "text": "SEARCH_TEXT"

#### Headers: 
- "Authorization": "TOKEN"

### Response 200

#### body
- "results": [{  
    "track_id": "TRACK_ID",  
    "track_title": "TRACK_TITLE",  
    "artist": {  
            "id": "ARTIST_ID",  
            "name": "ARTIST_NAME"  
            }, 
    "album": {  
        "id": "ALBUM_ID",  
        "name": "ALBUM_NAME"  
    },   
    "icon": "IMAGE_URL"  
    "lyrics": "NONE_OR_TEXT_OR_LRC"
    } ... ]

### Response 403
Not valid token

## GET /lyrics?track=TRACK_ID&type=TEXT_OR_LRC
#### Query parameters: 
- "track": "TRACK_ID"
- "type": "TYPE_OF_LYRICS"

#### Headers: 
- "Authorization": "TOKEN"

### Response 200
#### body
- {  
    "type": "TEXT / LRC",  
    "data": "LYRICS_CONTENT"  
    }

### Response 404
Track doesn't contain lyrics  

### Response 405
ONLY IF LRC  
Track contain TEXT lyrics, but not contain LRC