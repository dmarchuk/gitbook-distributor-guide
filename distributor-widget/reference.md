# Reference

## Options Reference {#options-reference}

> **Note:**
>
> Direct configuration of Distributor through the options has been deprecated and it will be disabled in future. Prefer to use Distributor Configuration in Commander. The only supported now are`configurationIds`and`openElements`.

| Name | Type | Default value | Description |
| :--- | :--- | :--- | :--- |
| configurationIds \(required\) | array of`string` | `''` | GUID of the used Distributor configurations.  You can get GUID of a configuration from it’s details page in Commander. The GUID is shown there as Identifier. |
| openElements | `string` | `''` | A list of comma-separated CSS selectors of elements, which will automatically get attached click event listeners for opening Distributor. The string is given as an argument to the`document.querySelectorAll`function, you get more info about its resemblance[here](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)for example.  The click event is being delegated, meaning that each element is being looked up on a website dynamically after the click happens. This way you can pass a selector to the elements that don’t exist yet during the initialization. |

## API Reference {#api-reference}

API calls are defined on the Distributor instance, which is created with the initialization call. This instance is returned to you as an argument of a callback function that you can pass as the second parameter to the initialization call. The following simple example shows how to use the calls to set up start and end dates, and then open the Distributor:

```javascript
<!-- Example of use of an instance to call the API -->
<script>
Mews.Distributor({
    configurationIds: ['aaaa-bbbb-cccc-dddd-eeeeeeee'],
}, function(distributor) {
   $('.booking-button').click(function() {
     var start = new Date();
     var end = new Date();
     end.setDate(start.getDate() + 2);

     distributor.setStartDate(start);
     distributor.setEndDate(end);
     distributor.open();
   });
});
</script>
```

Beware that API is slightly different in the\_Single\_and the\_Chain\_modes. The list of all API calls follows:

### Common API calls {#common-api-calls}

#### open\(\) {#open}

Opens Distributor in it’s overlay.

#### setLanguageCode\(languageCode\) {#setlanguagecodelanguagecode}

* `languageCode` Type: `string` - The languageCode to be set, in format `language-countryCode`, i.e`en-US`

Sets language of the Distributor’s localization. Language code should be in format`language-countryCode`, i.e.`en-US`as a variant of [IETF tag](https://en.wikipedia.org/wiki/IETF_language_tag). If a`languageCode`is not a in valid format, nothing happens.

#### setCurrencyCode\(currencyCode\) {#setcurrencycode}

* `currencyCode` Type: `string` - The currencyCode to be set, in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format, i.e`EUR`

Sets currency of the Distributor’s localization. Currency code should be in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format. If a`currencyCode` is not a in valid format, nothing happens.

#### setStartDate\(date\) {#setstartdatedate}

* `date` Type: `Date` - The start date to set

Sets start date for a new availability query, currently loaded availability list is not affected. If a`date`is not a valid Date object or its value isn’t allowed as start date - nothing happens.

#### setEndDate\(date\) {#setenddatedate}

* `date` Type: `Date` - The end date to set

Sets end date for a new availability query, currently loaded availability list is not affected. If a`date`is not a valid Date object - nothing happens.

#### setVoucherCode\(code\) {#setvouchercodecode}

* `code` Type: `string` - The voucher code to set

Sets a new voucher code value.

#### setRooms\(rooms\) {#setroomsrooms}

* `rooms` Type: `Array` - The list of GUIDs of rooms to be displayed \(see[`rooms`](https://mewssystems.github.io/public/content/distributor/widget/reference.html#rooms)option for more details\)

Sets a new list of the displayed room types, overwriting the initial Rooms option value. The currently loaded availability list is not affected.

### Only Single mode API calls {#only-single-mode-api-calls}

#### showRooms\(\) {#showrooms}

Sets Distributor to the`Rooms`step.

#### showRates\(roomId\) {#showratesroomid}

* `roomId` Type: `string` - an ID of a room to be selected \(see[`rooms`](https://mewssystems.github.io/public/content/distributor/widget/reference.html#rooms)option for more details about those Ids\)

Sets Distributor to the third step \(`Rates`\) as if you selected a room on the second screen.

### Only Chain mode API calls {#only-chain-mode-api-calls}

#### showHotels\(\) {#showhotels}

Sets Distributor to the`Hotels`step.

#### showRooms\(hotelId\) {#showroomshotelid}

* `hotelId` Type: `string` - an ID of a hotel which rooms you want to display

Sets Distributor to the`Rooms`step.

#### setCity\(cityId\)

* `cityId` Type: `string` - an ID of a city which hotels you want to display

### \(Optional\) Advanced configuration

As the third parameter, `Mews.Distributor` accepts optional configuration.

```javascript
Mews.Distributor(
    { configurationIds: ['aaaa-bbbb-cccc-dddd-eeeeeeee'] }, 
    function (dst) { dst.open(); },
    { dataBaseUrl: 'https://demo.mews.li' }
);
```

#### string dataBaseUrl

Allows you to define custom URL which is used for distributor API calls and static assets. In the example above, the Distributor will be run against our Demo environment.
