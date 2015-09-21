# Intro #

The geocodable plugin provides an easy way to present a text field to a user, and geocode their address input.  It currently uses google for geocoding, normalizing the placemark data from google and presenting a disambiguation popup if necessary.

# Requirements #

  1. Tested with jQuery 1.3.2
  1. Tested with Firefox 3.0/Linux, Firefox 3.5/Mac, Safari/Mac+Windows, IE 6.0+
  1. Google Maps API Key

# Usage #

## Javascript ##

You'll need to insure that the Google Maps API is pre-loaded so we have access to the Geocoder object.  At some future point the plugin could accept a key and auto-load the Google Map libraries, but it doesn't now.

Given the following code:

```
  <html>
    <body>
      <form>
        <input type="text" name="location" />
        <input type="submit" name="geocodeMe" />
      </form>
    </body>
  </html>
```

You can make the _location_ field geocodable (assuming you've already loaded the Google Maps library) by:

```
  <script type="text/javascript">
    //<![CDATA[
    $(document).ready(function() {
      $('#location').geocodable();
    });
    //]]>
  </script>
```

## Examples ##

Minimal examples can be seen here:  http://www.roarmouse.org/jquery-geocodable/index.html

## CSS ##

The code depends on two styles; the example above uses (these are slightly off for Safari, haven't tracked it down yet):

```
  .disambiguation {
    background-color: white;
    color: black;
    display: none;
    position: absolute;
    z-index: 1;
    padding: 0px 3px 3px 3px;
    border: 1px solid gray;
    border-top-width: 0px;
  }

  .disambiguationLink {
    margin: 0;
    border-bottom: 1px solid #ddd;
    padding: 2px;
    cursor: pointer;
    font-size: .8em;
  }
```

# Documentation #

See the code.  Options include:

  * disambiguationCallback: a function to present the results of geocoding if there are more than one
  * choiceCallback: a function to handle the users' choice after disambiguation
  * onSumbit: boolean, should geocoding fire on form.submit()
  * onBlur: boolean, should geocoding fire on field blur
  * submitOnFailure: boolean, should we submit even if geocoding failed
  * countries: countries we allow results from; any geocoded marks outside of these countries won't be presented
  * implicitCountries: countries we hide the country name for when showing addresses
  * baseCountryCode: override for browser-based country code when geocoding
  * mapCountry: whether to map a country abbreviation to a country name
  * mapRegion: whether to map a region abbreviation to a region name

# Issues #

  1. Internationalization is a huge problem here for the two 'map' options.
  1. The disambiguation callback can be handled better.
  1. Need to mark fields as "geocoded" so we don't re-geocode, though the local cache should mitigate this.
