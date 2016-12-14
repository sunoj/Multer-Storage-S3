# Multer-Storage-qiniu
Qiniu Multer Storage Engin

Multer Storage Engine that uses Qiniu as a storage system. Uses an offical Qiniu SDK.

## Installation
	
	npm install multer-storage-qiniu
	
## Dependencies
* qiniu   - for communication with the qiniu
* crypto  - for generating a pseudo random filename if one is not provided
* path    - for precise paths handling

## Usage
Multer-Storage-Qiniu follows the naming convention set by an existing DiskStorage storage engine that comes with multer.
```javascript
var multer = require( 'multer' );
var qiniu = require( 'multer-storage-qiniu' );
var storage = qiniu({
	destination : function( req, file, cb ) {
		
		cb( null, 'multer-uploads/my-files' );
		
	},
	filename    : function( req, file, cb ) {
		
		cb( null, file.fieldname + '-' + Date.now() );
		
	},
	config      :  {
		ACCESS_KEY: <YOUR_ACCESS_KEY>,
		SECRET_KEY: <YOUR_SECRET_KEY>,
		bucket: <BUCKET_NAME>,
	}
});
var uploadMiddleware = multer({ storage: storage });

app.post( '/upload', uploadMiddleware.single( 'attachment' ), function( req, res, next ) {

	res.send( 'File was uploaded successfully!' );

});
```


## License

[MIT](LICENSE)
