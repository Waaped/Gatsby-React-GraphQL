# Gatsby-React-GraphQL
Gatsby modular CSS and GraphQL

Great Gatsby Bootcamp FCC
https://www.youtube.com/watch?v=kzWIUX3CpuI

#1 Gatsby Project install

1. npm install -g Gatsby-cli@x.x.x
2. Gatsby new ‘Enter project Name’ https://github.com/gatsbyjs/gatsby-starter-hello-world
3. In package.json you can see the scripts available, we will start with ‘start’, npm run develop.
4. Local host 8000 manual start
5. 14:51 Next lesson

#2 Working with Gatsby Pages

1. Create pages, pages are automatically pathed in Gatsby localhost:8000/blog
    1. SRC>PAGES>BLOG.JS,INDEX.JS
2. Challenge consisted of creating pages in the same directory of index.js

#3 Linking between pages using Gatsby
1.       <p>need a developer? <a href="/contact">Contact me</a></p>
2. This is one way, Gatsby has other ways of optimizing this/faster/static
    1. import {Link } from 'gatsby'
    2. …
    3. <p>Need a developer? <Link to='/contact'>Contact me.</Link></p>
3. Link Gatsby component is the correct way of doing this, but <A> anchor tag is still valid for external website links
4. While the anchor tag  loads/reloads the page every time you click, Gatsby Preloads the page making it just as fast (Real time almost) as the click.
5. Challenge, external link to website/twitter/whatever, and about page links to contact page using Gatsby Link
    1. target=‘_blank’ for new browser tab when opening link, mine didn’t do that initially.
#4 Creating Shared Components
1. Creating a new component. option+G creates copyright in Mac, Just Normal React
2. As simple as it seems, we are beginning to USE dry methods that make it easy to update information across pages/components
3. Though I feel we Repeated ourselves too many times..

#5 Creating  Gatsby Page Layouts
1. Time for reusable page layouts I think! He calls it Universal Layout Component
2. We wrap the index.js unique information(Title, description) and remove non unique(Header/footer)
3. Then we add props as a parameter, and props.children to display the elements wrapped inside the layout component
import React from 'react';

const Layout =(props)=>{
    return(
        <div>
            {props.children}
        </div>
    )
}

//without props.chidlren the it would just display an empty div

export default Layout

4. Now we can import Header and footer into the Layout Div to DRY things up!

const Layout =(props)=>{
    return(
        <div>
            <Header/>
            {props.children} //child component text/divs
            <Footer/>
            
        </div>
5.  Doing this for the next components(about.js,blog.js)

#6 Styling for Gatsby Projects 1:00 hour mark

1. Adding CSS file, and importing it to Layout.css
2. Going through Gatsby packages in the gastbyjs.org, we will be installing sass
3. npm install gatsby-plugin-sass node-sass
4. Changed index.css into index.scss, Updated import on layout.js, used SCSS variable.

$color:green;

*{
    color:$color;
}

5. Links this page https://links.mead.io/gatsbystyles
    1. Copies entire css via RAW, and pastes into index.scss

#7 Stying Gatsby with css modules
1. CSS modules allow you to build complex styling, without the complexity.
2. We build a header.scss in the components folder, just for the header
3. Once we import the style into header, it is affecting the entire page, because the a tags are not scoped to the component
    1. We change the header.scss into modular scss. So the styling becomes dynamic. Header.module.scsss
    2. This stops the global CSS problems you had in Your Vendo App when you implemented the State managed component ‘CSS files in which all class names and animation names are scoped locally by default.’
        1. Inside header.js
					<ul><li><Link className={headerStyles.link} to='/'>Home</Link></li>
            1. He described it as dynamic
		2. Inside header.module.scss just a normal .link class 
		3. Creates another modular scss layout.module.scss
		4. Moving some divs around to deal with the footer, layout.syles.content, he did some advance css for the 			sticky footer
		5. More styling when you add a class name like .nav-list to react, you must include it like .headerStyles.navList 		in react camel case and it will render correctly.
		6.from 1:20 he starts styling navs,
			1. Most interesting jsx attribute he used was activeClassName, makes things easier for nav bar highlight

#8 Gatsby Data with GraphQL 1:28:25

1. Going into Gatsby-config.js          
2. 
3. module.exports = {
  /* Your site config here */
  siteMetadata:{
    title:'FullStack-Raf',
    author:'Rafael Vasquez'
  },
  plugins:[
    'gatsby-plugin-sass'
  ]
}

2. We can see what graphQL schema looks looks like at (GraphiQL) http://localhost:8000/___graphql
3. Importing graphQL, userStaticQuery from Gatsby
4. Restart the app and NPM run Build
5. In Header JS input a const inside the header like this, and call your data in the link h1 like this{}

import { Link, graphql,useStaticQuery } from 'gatsby';
import headerStyles from './header.module.scss'

const Header =() => {
    const data = useStaticQuery(graphql`
    query {
      site {
        siteMetadata {
          title / /We must specify the what piece of data/information we want in siteMetadata, in this case Title
        }
      }
    }
  `)
    return (
        <header className={headerStyles.header}>
            <h1>
                <Link className={headerStyles.title} to='/'>{data.site.siteMetadata.title}</Link>
1. By Importing graphQL and useStaticQuery we can keep data consistent across the app, and update information without repeating ourselves. Then we injected into the JSX.
2. Challenge: Put dynamic data into footer for author using the same techinque from the header component

#9 GraphQL Playground

1. Instead of using GraphiQL to test queries we will be installing GraphQL playground a newer solution
2. 1:47 mark, Just new IDE.
    1. npm install --save-dev env-cmd
    2. Create .env.development file in next to package.json in source
        1. Insert text GATSBY_GRAPHQL_IDE=playground into .env.dev
        2. In the package.json Change the develop line under scripts, 
        3. The Minus f was learned from a yt comment, should have googled myself the installation of the package
        4.  "develop": "env-cmd -f .env.development gatsby develop"
    3. The New GraphQl IDE UI is much better, and you can now have multiple tabs.


#10 Sourcing Content from the file system

1.Putting Data in our react components was great to demonstrate how GraphQL works, but for more complex/larger bits of information this will get a little clunky/bad

W-PED: gatsby-bootcamp raf$ npm install gatsby-source-filesystem@2.0.28

He creates a Posts file in the directory, and two md files
 	1. Gatsby.md and react.MD styled like a github readme
	2.  
