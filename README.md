# E-Commece Backend

## Description

Back end for an e-commerce site. Internet retail, also known as e-commerce, is the largest sector of the electronics industry, generating an estimated $29 trillion in 2019. E-commerce platforms like Shopify and WooCommerce provide a suite of services to businesses of all sizes.

## Table of Contents
- [Application Demo](#application-demo)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Code Snippet](#code-snippet)
- [Contributions](#contributions)
- [Questions](#questions)
- [License](#license)

## Application Demo

Link to an application demo: https://drive.google.com/file/d/1nqME2XA7NWDynwi84MoLWMDlNADpfp9F/view 

## Technologies Used

1. Javascript
2. Dotenv
3. Express
4. mysql2
5. Sequelize

## Installation

1. Clone this repo and open in IDE of choice.
2. Open terminal and nagivate to corresponding directory.
3. Run npm install to install dependencies.

## Usage

1. Log into mysql by typing `mysql -u root -p` into the command line and entering password.
2. Once logged in, create data base by typing `SOURCE ./db/schema.sql`. Exit mysql by entering `quit` into the command line.
3. Type `node seeds/index.js` to populate database
4. Type `node server.js` to connect to local host
5. Test all get, post, put, and delete routes using Insomnia

## Code Snippet

Following code was used to form our tables and columns.

```ruby
Product.init(
  {
    id: {
      type: DataTypes.INTEGER,
      allowNull: false,
      primaryKey: true,
      autoIncrement: true
    },
    product_name: {
      type: DataTypes.STRING,
      allowNull: false
    },
    price: {
      type: DataTypes.DECIMAL,
      allowNull: false,
      validate: {
        isDecimal: true
      },
    },
    stock: {
      type: DataTypes.INTEGER,
      allowNull: false,
      default: 10,
      validate: {
        isNumeric: true
      },
    },
    catergory_id: {
      type: DataTypes.INTEGER,
      references: {
        model: 'category',
        key: 'id',
      },
    },
  },
  {
    sequelize,
    timestamps: false,
    freezeTableName: true,
    underscored: true,
    modelName: 'product',
  }
);
```
This code is an example of our get route to access everything in our product table.

```ruby
router.get('/', async (req, res) => {
  try {
    const productData = await Product.findAll({
      include: [
        Category, {
          model: Tag,
          through: ProductTag,
     }
   ],
    });
    res.status(200).json(productData);
  } catch (err) {
    res.status(500).json(err);
  }
});
```

## Contributions

Mateo Navarro

Github: https://github.com/mateonav98 

LinkedIn: https://www.linkedin.com/in/mateonav

 ## Questions

For further information or any questions please contact me at mateonav98@gmail.com or https://github.com/mateonav98 

 ## License

MIT License

Copyright (c) 2022 Mateo Navarro

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.