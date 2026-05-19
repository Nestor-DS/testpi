# testpi

AIzaSyAM9IgbHnry4EvKFYQk8Np3TMKvHDGZT18

14899dcf299b58cf2b25ee5c

const GoogleMapsLoader = (() => {

    const GOOGLE_MAPS_URL =
        "https://maps.googleapis.com/maps/api/js?key=API_KEY&loading=async&libraries=places";

    let loadingPromise = null;

    function load() {

        if (loadingPromise) {
            return loadingPromise;
        }

        loadingPromise = new Promise((resolve, reject) => {

            const script = document.createElement("script");

            script.src = GOOGLE_MAPS_URL;

            script.async = true;
            script.defer = true;

            script.onload = () => {

                if (!window.google || !window.google.maps) {
                    reject(new Error("Google Maps no disponible"));
                    return;
                }

                resolve(window.google.maps);
            };

            script.onerror = () => {
                reject(new Error("Error cargando Google Maps"));
            };

            document.head.appendChild(script);
        });

        return loadingPromise;
    }

    return {
        load
    };

})();

___________

<div id="map" style="width:100%; height:400px;"></div>

<script>
    function initMap() {
        const map = new google.maps.Map(document.getElementById("map"), {
            center: { lat: 19.4326, lng: -99.1332 },
            zoom: 14
        });

        // Si el contenedor estaba oculto o se cargó tarde:
        setTimeout(function () {
            google.maps.event.trigger(map, "resize");
            map.setCenter({ lat: 19.4326, lng: -99.1332 });
        }, 300);
    }
</script>

<script 
    src="https://maps.googleapis.com/maps/api/js?key=TU_API_KEY&callback=initMap"
    async
    defer>
</script>