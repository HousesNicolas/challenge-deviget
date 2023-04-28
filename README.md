# challenge-deviget

Manual Setup

# Create your project directory then go into it:
mkdir -p ~/Sites/magento
cd $_

# Download the Docker Compose template:
curl -s https://raw.githubusercontent.com/markshust/docker-magento/master/lib/template | bash

# Download the version of Magento you want to use with:
bin/download 2.4.6 community

# Replace with existing source code of your existing Magento instance:
git clone git@github.com:HousesNicolas/challenge-deviget.git

# Start some containers, copy files to them and then restart the containers:
bin/start --no-dev

# If your vendor directory was empty, populate it with:
bin/composer install

# Drop and create current database
bin/mysql
drop database magento;
create database magento;

# Import existing database:
bin/mysql < magento2db.sql

# Import app-specific environment settings:
bin/magento app:config:import

# Create a DNS host entry and setup Magento base url
bin/setup-domain magento.test

# Disable module
bin/magento module:disable Magento_TwoFactorAuth Magento_AdminAdobeImsTwoFactorAuth

bin/restart

bin/magento setup:upgrade; bin/magento s:d:c ; bin/magento setup:static-content:deploy -f ; bin/magento cache:flush

open https://magento.test

---------------------------------------------------------------------------------------------

Admin Configuration
User: admin
Password: 123456aA

# Setup Slider
In the admin menu:
Go to MAGICCART > Slider
Click on: Identifier home_slider > Edit
On “Images And Videos”  click “Browse to find or drag image here” to add images for the slider
The images are in challenge-deviget .../src/pub/media/wysiwyg/mens
These images are for desktop:
my-profile.png
people-1.png
people-3.png

On “Images And Videos For Mobile”  click “Browse to find or drag image here” to add images for the slider
The images are in challenge-deviget .../src/pub/media/wysiwyg/mens
These images are for Mobile:
my-profile-mob.png
people-1-mob.png
people-3-mob.png

After all click “Save Magicslider”

The widgets was added in Home page 
In the admin menu:
Go to CONTENT > Elements > Pages > Select > Edit “ Home page”
Then click “Edit with Page Builder” and you can see the code.
-----------------------------------------------------------------------------------------------------------

On the home page we have the slider, which has a link to the presentation page https://magento.test/magento-professional-developer

-----------------------------------------------------------------------------------------------------------

In the admin menu:
Go to CATALOG > Products
Search “My Deviget Bag”

Configurable product url: https://magento.test/my-deviget-bag.html
Backend configurable product:
Name: My Deviget Bag
Go to “Images And Video” and click “Browse to find or drag image here”
These images are:
leather-duffle-bag-1028_1.png
leather-duffle-bag-1028_2.png
leather-duffle-bag-1028_4.png

------------------------------------------------------------------------------------------------------------

Talking about yourself as a Magento Professional developer

CMS page: https://magento.test/magento-professional-developer

In the admin menu:
Go to CONTENT > Elements > Pages > Select > Edit “ Magento Professional developer”
Then click “Edit with Page Builder” and you can see the code.
