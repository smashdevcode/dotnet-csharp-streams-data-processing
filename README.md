
# C# Streams and Data Processing

## Bing Search API Updates

## Video 3 - Searching for News Headlines

### Bing News Search API v7

Information for the Bing News Search API (v7) can be found at:

[https://azure.microsoft.com/en-us/services/cognitive-services/bing-news-search-api/](https://azure.microsoft.com/en-us/services/cognitive-services/bing-news-search-api/)

Using the preview tool on the Bing News Search API home page, we can see that the order of the JSON elements has changed a bit, but the elements that are used in the videos are still present.

```
{
  "_type": "News",
  "readLink": "https://api.cognitive.microsoft.com/api/v7/news/search?q=football",
  "totalEstimatedMatches": 6260000,
  "value": [
    {
      "about": [
        {
          "readLink": "https://api.cognitive.microsoft.com/api/v7/entities/6ff32734-2ab0-2636-a1b0-1e2f5e94a701",
          "name": "National Football League"
        }
      ],
      "provider": [
        {
          "_type": "Organization",
          "name": "Orlando Sentinel"
        }
      ],
      "datePublished": "2018-01-23T00:08:00Z",
      "clusteredArticles": null,
      "mentions": null,
      "video": {
        "name": "NFL to honor undefeated UCF football team during Pro Bowl",
        "thumbnailUrl": "https://www.bing.com/th?id=ON.AA0B7CC356617768F42D4E293487E932&pid=News",
        "allowHttpsEmbed": false,
        "thumbnail": {
          "contentUrl": null,
          "width": 480,
          "height": 270
        }
      },
      "category": "Sports",
      "name": "NFL to honor undefeated UCF <b>football</b> team during Pro Bowl",
      "url": "http://www.orlandosentinel.com/sports/ucf-knights/knights-notepad/os-sp-ucf-pro-bowl-0123-story.html",
      "description": "The NFL plans to recognize UCF’s 13-0 undefeated <b>football</b> season during the 2018 Pro Bowl at Camping World Stadium Sunday. Players have been invited to walk out on the field for a celebration after the first quarter. “When we thought about UCF and the ...",
      "image": {
        "contentUrl": null,
        "thumbnail": {
          "contentUrl": "https://www.bing.com/th?id=ON.9804C1756EBB5424E44D51A52DF2A21D&pid=News",
          "width": 700,
          "height": 393
        }
      }
    }
  ]
}
```

The documentation for v7 of the API can be found at:

[https://docs.microsoft.com/en-us/azure/cognitive-services/bing-news-search/](https://docs.microsoft.com/en-us/azure/cognitive-services/bing-news-search/)

### Obtaining API Keys

You can obtain keys for v7 of the API by visiting the "Try Cognitive Services" page at:

[https://azure.microsoft.com/en-us/try/cognitive-services/?api=bing-news-search-api](https://azure.microsoft.com/en-us/try/cognitive-services/?api=bing-news-search-api)

Under the "Select API" section, click the "Get API Key" button located to the right of the "Bing Search APIs v7" subsection.

__Please note that the API keys that you'll obtain for v7 of the API will only work with that version of the API (and not v5 of the API).__

### Creating the JSON Classes

The C# quickstart for the Bing News Search API can be found at:

[https://docs.microsoft.com/en-us/azure/cognitive-services/bing-news-search/csharp](https://docs.microsoft.com/en-us/azure/cognitive-services/bing-news-search/csharp)

On the quickstart page, you can find an example of the response from the Bing News Search API. The JSON sample provides a "Copy" button that allows you to easily copy the JSON to your clipboard. After you copy the JSON to your clipboard, follow the steps shown in the video to create your JSON classes.

### Updating the `Program` Class

All of the steps shown in the video to create the `GetNewsForPlayer` are unchanged, with one notable exception: the URL for the API has changed to `https://api.cognitive.microsoft.com/bing/v7.0/news/search?q={0}`.

The code for the finished WebClient `DownloadData` method call should look like this:

```
byte[] searchResults = webClient.DownloadData(
	string.Format("https://api.cognitive.microsoft.com/bing/v7.0/news/search?q={0}", playerName));
```

## Video 4 - Deserialize the News Results

All of the steps shown in the video are unchanged. For some reason, when uncommenting the code in the `Main` method, all of the text had been converted to lowercase text. To get the project to build, I had to update the code for the `Main` method to this:

```
string currentDirectory = Directory.GetCurrentDirectory();
DirectoryInfo directory = new DirectoryInfo(currentDirectory);
var fileName = Path.Combine(directory.FullName, "SoccerGameResults.csv");
var fileContents = ReadSoccerResults(fileName);
fileName = Path.Combine(directory.FullName, "Players.json");
var players = DeserializePlayers(fileName);
var topTenPlayers = GetTopTenPlayers(players);
foreach (var player in topTenPlayers)
{
	Console.WriteLine("Name: " + player.FirstName + " PPG: " + player.PointsPerGame);
}
fileName = Path.Combine(directory.FullName, "topten.json");
SerializePlayersToFile(topTenPlayers, fileName);
```
