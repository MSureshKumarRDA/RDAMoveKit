# RDAMoveKit
Track user location in background
Download this movekit.aar library and setup with your project
We need some uses permission to access background location, So please follow the below code

    if (PermissionUtils.requestPermissionForLocationAccess(this)) {     
      startMoveKit();        
    }
 
    private void startMoveKit() {
 
        MoveKit.initialize(this, "83cffa2e7b8a8ebe1ad3fd1641ddb0c3");
        
        MoveKit.startLocationAccess(this, new LocationAccessStartListener() {
            @Override
            public void locationAccessSuccess(String res) {
                Toast.makeText(getApplicationContext(), res, Toast.LENGTH_SHORT).show();
            }

            @Override
            public void locationAccessFailed(String res) {
                Toast.makeText(getApplicationContext(), res, Toast.LENGTH_SHORT).show();
            }
          });
        }
        
        "83cffa2e7b8a8ebe1ad3fd1641ddb0c3" -> This is company registeration token. You can register in http://www.rudram.co/ 
    
 Add below code in onActivityResult()   
 
        if ((requestCode == MoveService.REQUEST_CHECK_SETTINGS) && (resultCode == Activity.RESULT_OK)) {
            startMoveKit();
        }
        
 Add below code in onRequestPermissionsResult()
 
      if (requestCode == PermissionUtils.MANDATORY_FOR_MOVE_KIT_REQUEST) {
            Map<String, Integer> map = new HashMap<>();
            map.put(android.Manifest.permission.ACCESS_FINE_LOCATION, PackageManager.PERMISSION_GRANTED);
            map.put(android.Manifest.permission.ACCESS_COARSE_LOCATION, PackageManager.PERMISSION_GRANTED);
            map.put(android.Manifest.permission.READ_PHONE_STATE, PackageManager.PERMISSION_GRANTED);
                for (int i = 0; i < grantResults.length; i++) {
                    map.put(permissions[i], grantResults[i]);
                }
                if ((map.get(android.Manifest.permission.ACCESS_FINE_LOCATION) == PackageManager.PERMISSION_GRANTED) &&     (map.get(android.Manifest.permission.ACCESS_COARSE_LOCATION) == PackageManager.PERMISSION_GRANTED) && (map.get(android.Manifest.permission.READ_PHONE_STATE) == PackageManager.PERMISSION_GRANTED)) {
                startMoveKit();
                } else {
                Toast.makeText(getApplicationContext(), "Sorry! you cannot access due to lack of permission", Toast.LENGTH_SHORT).show();
            }
        }

