TODO: PRETTY PICTURE
- HTTP Request -- Request Parser --> Operation
- HTTP Request -- Credentials Extractor --> Credentials
- Operation -- Modes Extractor --> AccessModes
- Credentials, Operation -- Permission Reader --> Permissions
- Credentials, Operation, Permissions -- Authorizer --> Reject/Accept request
- Operation -- Operation Handler --> Response Description
- Error -- Error Handler --> Response Description
- HTTP Response, Response Description -- Response Writer --> Write HTTP Response
