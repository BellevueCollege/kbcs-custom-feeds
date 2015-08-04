# KBCS App Customizations Plugin

This plugin provides two pieces of functionality need for the KBCS iOS app.

- [Custom feeds](#custom-feeds)
- [Single episode URL/page](#single-episode)

##<a name="custom-feeds"></a>Custom feeds

The plugin provides for custom Wordpress feeds which utilize the Playlist Center API. The custom feeds integrate show/episode information from the Playlist Center with program information from the KBCS Wordpress website.

The plugin adds an additional feed endpoint of `episodes` which can currently be used in two scenarios.

### Program feed

- **Template URL:** http://kbcs.fm/programs/[program-name]/episodes
- **Example usage:** http://kbcs.fm/programs/democracy-now/episodes
- **What it does:** It gets a feed of the last `x` shows for the provided program.

### Program type aggregate feed

- **Template URL:** http://kbcs.fm/program_type/[program-type]/episodes
- **Example usage:** http://kbcs.fm/program_type/music/episodes
- **What it does:** It provides an aggregate feed of the last `x` shows for all programs (combined) of the given program type.

>Note: Be wary of usage. This feed is weird to generate as there is currently not a way in the Playlist Center API to pull program show information in aggregate. This feed does its best version of it by getting the last 20 shows for each program, aggregating all those items, sorting, then slicing off the number requested. As it is not a true aggregate, be cautious of using results past the first 40-60.

### Customizable options

#### Item count
An additional request parameter of `itemCount` and value can be added to the URL to alter the number of returned items in the feed.

- **Example:** http://kbcs.fm/programs/democracy-now/shows?itemCount=30

If this parameter/value is not provided, the feed will return the default number of items as set in the Wordpress site options.

#### Paging
_Available only for program type aggregate feed._ An additional request parameter of `page` and value can be added to the URL 

- **Example:** http://kbcs.fm/programs/democracy-now/shows?itemCount=30&page=2

If this parameter/value is not provided, the feed will by default return the first `x` number of results (as defined by default or provided `itemCount`).

## <a name="single-episode"></a>Single episode URL/page

The plugin provides for serving a page specific to a single program episode. This page is used within the iOS app to display information about an episode. As such, it is expected to be used in a mobile/tablet device context and is not for use within the greater KBCS website.

- **Template URL:** http://kbcs.fm/episode-page/[showId]
- **Example usage:** http://kbcs.fm/episode-page/43744