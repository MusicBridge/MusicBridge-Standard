# Endpoints for MBs-1.0

## GET /
### Response 200
#### body
- "supported_standard_versions": ["MBs-X.X"]
- "provider_identifier": "SERVICE_NAME"
- "provider_repository": "LINK_TO_PROVIDER_GITHUB_REPOSITORY"

## GET /v1.0/

#### Headers: 
- "Authorization": "TOKEN"

### Response 200
#### body

- "premium": Boolean
- "logo": "IMAGE_URL"
- "colors": {    
        "foreground": "HEX_COLOR",  
        "background": "HEX_COLOR",  
        "highlight": "HEX_COLOR"  
    }

## GET /v1.0/auth

### Response 200
#### body

- "auth_url": "URL"

## GET /v1.0/search?text=DATA
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
        "name": "ALBUM_NAME",  
        "logo": "IMAGE_URL"  
    },   
    "lyrics": ("NONE", "TEXT", "LRC"),  
    "warnings": ["NONE", "EXPLICIT", "REGION"]  
    } ... ]

### Response 403
#### body
- "error": "invalid_token"
- "message": "Authorization token is invalid or expired"

## GET /v1.0/lyrics?track=TRACK_ID&type=TEXT_OR_LRC
#### Query parameters: 
- "track": "TRACK_ID"
- "type": ("TEXT", "LRC")

#### Headers: 
- "Authorization": "TOKEN"

### Response 200
#### body
- "type": ("TEXT", "LRC")  
- "data": "LYRICS_CONTENT"  

### Response 403
#### body
- "error": "invalid_token"
- "message": "Authorization token is invalid or expired"

### Response 404
#### body
- "error": "no_found"
- "message": "Track doesn't contain lyrics"

### Response 422
#### body
- "error": "no_found_by_type"
- "message": "Track contain TEXT lyrics, but not contain LRC"