# Endpoints for MBs-1.0

## GET /
### Response 200
#### body
- "supported_standard_versions": ["MBs-X.X"]
- "provider_identifier": "SERVICE_NAME"
- "provider_repository": "LINK_TO_PROVIDER_GITHUB_REPOSITORY"
- "logo": "IMAGE_URL"
- "color": "HEX_COLOR"

## GET /v1.0/

#### Headers: 
- "Authorization": "TOKEN"

### Response 200
#### body

- "premium": Boolean

### Response 401
*Bad or empty token*
#### body
- "detail": "Bad Token"

## GET /v1.0/auth

### Response 200
#### body

- "auth_url": "URL"

## GET /v1.0/search/%DATA%
### Request

#### Parameters: 
- %DATA%: "SEARCH_TEXT OR trackId:TRACK_ID"

#### Headers: 
- "Authorization": "TOKEN"

### Response 200

#### body
- [{  
    "id": "TRACK_ID",  
    "title": "TRACK_TITLE",  
    "url": "TRACK_URL",
    "artist": {  
        "id": "ARTIST_ID",  
        "url": "ARTIST_URL",
        "name": "ARTIST_NAME"  
    }, 
    "album": {  
        "id": "ALBUM_ID",  
        "url": "ALBUM_URL",
        "name": "ALBUM_NAME",  
        "logo": "IMAGE_URL"  
    },   
    "lyrics": {
        "text": Boolean,
        "lrc": Boolean
    },  
    "explicit": False,
    } ... ]

### Response 401
*Bad or empty token*
#### body
- "detail": "Bad Token"

## GET /v1.0/lyrics/%TYPE%/%TRACK_ID%
#### Parameters: 
- "%TYPE%": "TEXT/LRC"
- "%TRACK_ID%": "TRACK_ID"

#### Headers: 
- "Authorization": "TOKEN"

### Response 200
#### body
- {  
    "type": "TEXT/LRC"
    "lyrics": "LYRICS"
    }

### Response 401
*Bad or empty token*
#### body
- "detail": "Bad Token"

### Response 403
*Premium subscription required*
#### body
- "detail": "Premium subscription required"

### Response 404
*Bad or empty track id*
#### body
- "detail": "Track not found"

### Response 405
*This lyrics type are not avaliable*
#### body
- "detail": "This lyrics type are not avaliable"
