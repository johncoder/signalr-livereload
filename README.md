## SignalR Live Reload ##

This is my in-flight project for trying out [scriptcs](http://github.com/scriptcs/scriptcs). I was already working on a little console app to facilitate live reload in a SignalR app. This just makes it awesome.

**Note:** I might have a couple of unnecessary references in the project, but I'll straighten it out later. Just stoaked I got this working at all!

## Getting Started ##

In *your* project that uses SignalR, add the following hub:

    [HubName("liveReload")]
    public class LiveReloadHub : Hub
    {
        public void ReloadAllClients()
        {
            Clients.Others.reload();
        }
    }

Then, add the relevant markup to your Razor layout:

    <script src="/Scripts/jquery-1.6.4.min.js"></script>
    <script src="/Scripts/jquery.signalR-1.0.1.min.js"></script>
    <script src="/signalr/hubs"></script>
    <script type="text/javascript">
        $(function () {
            var hub = $.connection.liveReload;

            hub.client.reload = function () {
                console.log("reloading!");
                document.location.reload(true);
            };

            $.connection.hub.start().done(function () {
                console.log("ready");
            });
        });
    </script>

## Running the Live Reloader ##

1. Set up scriptcs (no worries, it's easy).
2. Run `nuget install -o packages` to restore the packages listed in `packages.config`.
3. Run `scriptcs signalr.livereload.csx`
4. Edit `config.json` and fill in the blanks.
5. Run `scriptcs signalr.livereload.csx` again.
