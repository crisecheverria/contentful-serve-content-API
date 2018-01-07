# Contentful: Serve content API
In this repo I write about Contentful.com a very useful service where users can serve content to any device.

In this modern world about web development, almost all web companies are providing API's to theirs users and the main reason for that is to provide/serve content to almost any device; Desktop, Mobile, Tablets, VR and much more to comes. So I read a Medium Blog post about [Hos to use API first platforms to build your website faster](https://medium.freecodecamp.org/how-to-use-api-first-platforms-to-build-your-websites-faster-e917e8318ee) and the author use a great and new tool for me called [Contentful.com](https://www.contentful.com/) as they say in their site you can just "Ship your digital products faster
Remove content bottlenecks and enable developers and content creators to do their best work, together."

## Create Models
With Contentful, you can create Models in order to store your data, for example you can create **Experts** and **Technology** Models and also you can define **Fields** from 1 - 50 fields and the fields can be: Text, Number, Date and Time, Location, Media, Boolean, JSON Object, Reference

![ContentFul Fields](https://github.com/crisecheverria/contentful-serve-content-API/blob/master/images/contentful-fields.png)

Once you created your Content Model with his fields, then you can add content. Contentful provide a simple but great CMS in order to add your content, think just the same as Wordpress or any other CMS out there. Also you can choose the locale for every content `en-US` is the default locale.

![ContentFul CMS](https://github.com/crisecheverria/contentful-serve-content-API/blob/master/images/contentful-cms.png)

## Contentful Javascript SDK
Now, you can integrate your Models to your project using their [Javascript SDK](https://github.com/contentful/contentful.js)

### Node
Using npm:
```
npm install contentful
```
### Yarn
Using npm:
```
yarn add contentful
```
### Browser
For browsers, contentful recommend to download the SDK vá npm or yarn to ensure 100% availability.
```
<script src="https://cdn.jsdelivr.net/npm/contentful@latest/dist/contentful.browser.min.js"></script>
```
## Retrieve Data
Now for fetch data you can use the next code:
```javascript
<script type="text/javascript">

  // Contentful API SpaceId and accesToken. You have to create your own SpaceId and accesToken inside the API header Menu
  const client = contentful.createClient({
    space: '2i6v00l3evd1',
    accessToken: 'accdba3b0feedb0bb595e8e788e85860db650c44be74f46d4eaa7dc733bb6b5c'
  })

  function fetchTechnologies () {
    // Contentful provide the getEntries method from where you can fetch your Content Model data.
    return client.getEntries({
        content_type: "technology" // This is the name of one of my Content Model
      })
    .then((response) => response.items)
    .catch((error) => {
      console.log(`\nError occurred while fetching Entries for Technology:`)
      console.error(error)
    })
  }

  fetchTechnologies().then((technologies) => {
    
    // Using Vanilla Javascript and Array Map Method we can publish our content in our HTML page
    techCards.innerHTML += technologies.map(technology => 
      `<div class="col-md-4">
        <div class="card">
          <a href="${technology.fields.link}"><img src="${technology.fields.logo.fields.file.url}" class="small-logo" /></a>
          <h2><a href="/experts.html?t=${technology.fields.name}">${technology.fields.name}</a></h2>
          <p>${technology.fields.description}</p>
        </div>
      </div>`).join('')
  })
</script>
```