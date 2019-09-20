<template>
    <section class="about container">
        <h2 class="about-title-top" id="Aboutme">Let's get ac quainted</h2>
        <div class="about-top flex-container">
            <div class="about-img">
                <img src="../assets/imgs/man-mobile.svg" alt="man-mobile" class="lazy">
            </div>
            <div class="about-info">
                <h3 class="about-subtitle">I am cool frontend developer</h3>
                <p class="about-text">When real users have a slow experience on mobile, they're much less likely to find what they are looking for or purchase from you in the future. For many sites this equates to a huge missed opportunity, especially when more than half of visits are abandoned if a mobile page takes over 3 seconds to load.</p>
                <p class="about-text">Last week, Google Search and Ads teams announced two new speed initiatives to help improve user-experience on the web. </p>
                <a href="#SignUp" class="about-sign-up">Sign Up</a>
            </div>
        </div>
        <div class="about-bottom">
            <h2 class="about-title" id="Relationship">About my relationships with web-development</h2>
            <ul class="about-list flex-container">
                <li class="about-list-item">
                    <div class="about-image-lang">
                        <img src="../assets/imgs/html.svg" alt="html" class="lazy">
                    </div>
                    <div class="about-container">
                        <h3 class="about-subtitle">I'm in love with HTML</h3>
                        <p class="about-text">Hypertext Markup Language (HTML) is the standard markup language for creataing web pages and web applications.</p>
                    </div>
                </li>
                <li class="about-list-item">
                    <div class="about-image-lang">
                        <img src="../assets/imgs/css.svg" alt="css" class="lazy">
                    </div>
                     <div class="about-container">
                         <h3 class="about-subtitle">CSS is my best friend</h3>
                         <p class="about-text">Cascading Style Sheets (CSS) is a  style sheet language used for describing the presentation of a document written in a markup language like HTML.</p>
                     </div>
                </li>
                <li class="about-list-item">
                    <div class="about-image-lang">
                        <img src="../assets/imgs/javascript.svg" alt="javascript" class="lazy">
                    </div>
                    <div class="about-container">
                        <h3 class="about-subtitle">JavaScript is my passion</h3>
                        <p class="about-text">JavaScript is a high-level, interpreted programming language. It is a language which is also characterized as dynamic, weakly typed, prototype-based and multi-paradigm.</p>
                    </div>
                </li>
            </ul>
        </div>
    </section>
</template>
<script>
    export default {
        data(){
            return {

            }
        }
    }
</script>