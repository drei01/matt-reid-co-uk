---
layout: post
title: android google maps v2 MapView inside a fragment
---

The [google maps
v2](https://developers.google.com/maps/documentation/android/) library
for android provides some much needed features for your app such as
MapFragments. There is also a new support library to provide these
features to older versions of android.








The problem comes when you want to include a mapview in your own custom
fragment (i.e you don"t want the map to be the full size of the view).










The solution is pretty hard to find and not all of it is documented. You
must call all the lifecycle methods (onCreate, onResume) as well as the
static maps Initializer method.










Custom Fragment Class










    public class CustomMapFragment extends Fragment {
        
        private MapView mMapView;
        private GoogleMap googleMap;
        
        @Override
        public View onCreateView(LayoutInflater inflater, ViewGroup container, 
                Bundle savedInstanceState) {
            // inflat and return the layout
            View v = inflater.inflate(R.layout.map_fragment, container, false);
            mMapView = (MapView) v.findViewById(R.id.mapView);
            mMapView.onCreate(savedInstanceState);
            mMapView.onResume();//needed to get the map to display immediately
            
            try {
                MapsInitializer.initialize(this);
            } catch (GooglePlayServicesNotAvailableException e) {
                e.printStackTrace();
            }
            
            googleMap = mMapView.getMap();
            
            //Perform any camera updates here
            
            return v;
        }
        
        @Override
        public void onResume() {
            super.onResume();
            mMapView.onResume();
        }
        
        @Override
        public void onPause() {
            super.onPause();
            mMapView.onPause();
        }
        
        @Override
        public void onDestroy() {
            super.onDestroy();
            mMapView.onDestroy();
        }
        
        @Override
        public void onLowMemory() {
            super.onLowMemory();
            mMapView.onLowMemory();
        }
    }





 Layout file



 









