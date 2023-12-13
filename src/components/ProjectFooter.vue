<template>
    <body>
        <footer>
            <div class="f-item-con">
                <div class="app-info">
                    <span class='app-name'>
                    CS 630 (005) Fall 2023 - Group 10
                    </span>
                    <p><strong>TEXT EDITOR</strong></p>
                    <p>A text editor is a type of computer program that edits plain text.
                        Text editors are provided with operating systems and software
                        development packages, and can be used to change files such as
                        configuration files, documentation files and programming
                        language source code.</p>
                </div>
                <div class="useful-links">
                    <div class="footer-title">Group members</div>
                    <ul>
                        <li>Samshad Tabrez Shaik</li>
                        <li>Richa Singh</li>
                        <li>Ananya Kishore Kumar Yajaman</li>
                        <li>Vaishnavi Masapalli</li>
                    </ul>
                    <a href="https://github.com/tabrezdn1/cs630-text-editor" target="_blank" style="color: white;">Source code</a>
                </div>

                <div class="g-i-t">
                    <div class="footer-title">Under Guidance of</div>
                    <img src="./prof.png" height="100px" />
                    <div class="footer-title">Prof. Larry Lay</div>
                </div>
            </div>
        </footer>

    </body>
</template>

<style scoped >
footer {
    background-color: #111010;
    margin-top: 50px;
}

.f-item-con {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    grid-gap: 2rem;
}

footer .app-name {
    color: white;
    border-left: 4px solid var(--theme-col);
    padding-left: 1rem;
    font-size: 1.875rem;
}

.app-name .app-initial {
    color: var(--theme-col);
}

footer .app-info p {
    color: white;
    padding-left: 1.65rem;
}

footer .footer-title {
    font-size: 1.25rem;
    color: white;
    border-left: 4px solid var(--theme-col);
    padding-left: 1.5rem;
    height: fit-content;
}

footer ul {
    padding-left: 1.75rem;
    color: white;
    font-size: 0.875rem
        /* 14px */
    ;
    line-height: 1.25rem;
    margin-top: .5rem;
}

footer ul li {
    margin: .25rem 0;
    cursor: pointer;
    color: #d4d4d4;
    width: fit-content;
}

footer ul li:hover {
    color: white;
}

footer .help-sec {
    grid-column-start: 2;
}

footer .cr-con {
    background-color: #232127;
    color: white;
    padding: 1rem 4rem;
    text-align: center;
}</style>