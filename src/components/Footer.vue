<template>
    <footer id="footer">
        <div class="container">
            <div class="footer-top flex-container">
                <div class="logo">
                    <a href="#">
                        <img src="../assets/logo/logo.png" alt="logo">
                    </a>
                </div>
                <ul class="footer-menu flex-container">
                    <li class="footer-menu-item" v-for="(menuItem,index) in menu" :key="index"><a :href="menuItem.url">{{menuItem.pageName}}</a></li>
                </ul>
            </div>
            <div class="footer-middle flex-container">
                <ul class="footer-contacts-list">
                    <li class="contacts-list-item"><a href="mailto:work.of.future@gmail.com" class="contacts-mail">work.of.future@gmail.com</a></li>
                    <li class="contacts-list-item"><a href="tel:+380507892498" class="contacts-tel">+38 (050) 789 24 98</a></li>
                    <li class="contacts-list-item"><a href="tel:+380955560845" class="contacts-phone">+38 (095) 556 08 45</a></li>
                </ul>
                <ul class="footer-submenu">
                    <li class="footer-submenu-item" v-for="(subItem,index) in submenu" :key="index"><a :href="subItem.url">{{subItem.pageName}}</a></li>
                </ul>
            </div>
            <div class="footer-bottom flex-container">
                <div class="copyright">© abz.agency specially for the test task</div>
                <ul class="footer-social-menu flex-container">
                    <li class="footer-social-menu-item"><a href="#"><img src="../assets/icons/facebook.svg" alt="facebook"></a></li>
                    <li class="footer-social-menu-item"><a href="#"><img src="../assets/icons/linkedin.svg" alt="linkedn"></a></li>
                    <li class="footer-social-menu-item"><a href="#"><img src="../assets/icons/twitter.svg" alt="twitter"></a></li>
                    <li class="footer-social-menu-item"><a href="#"><img src="../assets/icons/pinterest.svg" alt="pinterest"></a></li>
                </ul>
            </div>
        </div>
    </footer>
</template>

<script>
    export default {
        data(){
            return {
                menu: [
                    {url: '#Aboutme',pageName: 'About me'},
                    {url: '#Relationship',pageName: 'Relationships'},
                    {url: '#Requirements',pageName: 'Requirements'},
                    {url: '#Users',pageName: 'Users'},
                    {url: '#SignUp',pageName: 'Sign Up'}
                ],
                submenu: [
                    {url: '#',pageName: 'News'},
                    {url: '#',pageName: 'Blog'},
                    {url: '#',pageName: 'Partners'},
                    {url: '#',pageName: 'Shop'},
                    {url: '#',pageName: 'Overview'},
                    {url: '#',pageName: 'Design'},
                    {url: '#',pageName: 'Code'},
                    {url: '#',pageName: 'Collaborate'},
                    {url: '#',pageName: 'Tutorials'},
                    {url: '#',pageName: 'Resources'},
                    {url: '#',pageName: 'Guides'},
                    {url: '#',pageName: 'Examples'},
                    {url: '#',pageName: 'FAQ'},
                    {url: '#',pageName: 'Terms'},
                    {url: '#',pageName: 'Conditions'},
                    {url: '#',pageName: 'Help'}
                ]
            }
        }
    }
</script>

