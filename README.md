# Kitty 33

Unfortunately I last minuted did the web challenge due to my busy schedule. But here is my solution towards this challenge.

#### First, click on http://45.33.123.243:5020/

You will see the classic vulnerable login page. And immediately I taught of using SQL injections. So I used the payload SQL injection list. Thanks, Ismail.

https://github.com/payloadbox/sql-injection-payload-list

![Login Page](blob:https://imgur.com/dDPPwg2)

Inserted both username and password with this payload:
```
' OR '' = '

```
And click login.

#### After that, you will see this dashboard page. 

![Dashboard Page](blob:https://imgur.com/6q7YtRc)

The reason I know there is a dashboard page is because I inspect element the source codes which are provided. You can refer to the index, script.js and style.css for viewing.

#### Inspect element the dashboard page. Refer to the dashboard files given.

Inside of the dashboard html page, I noticed that there is a script part where it stated "cat flag.txt" 

dashboard.html:

    <script>
    function addPost(event) {
        event.preventDefault();
        const post_in = document.getElementById('post_input').value;
        
        if (post_in.startsWith('cat flag.txt')) {
            fetch('/execute', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded'
                },
                body: `post_input=${encodeURIComponent(post_in)}`
            })
            .then(response => response.text())
            .then(result => {
                const contentSection = document.querySelector('.content');
                const newPost = document.createElement('div');
                newPost.classList.add('post');
                newPost.innerHTML = `<h3>Flag Post</h3><p>${result}</p>`;
                contentSection.appendChild(newPost);
            });
        } else {
            const contentSection = document.querySelector('.content');
            const newPost = document.createElement('div');
            newPost.classList.add('post');
            newPost.innerHTML = `<h3>User Post</h3><p>${post_in}</p>`;
            contentSection.appendChild(newPost);
        }
    }
</script>

so I excited copy and paste it to the post and execute it right away.

And woohoo, we got the flag.

![Flag Secured](blob:https://imgur.com/zDuzEjK)


### In conclusion, although I am late to the party but hey at least I managed to do one web challenge in time. But sadly I couldn't submit in time lmao.









# KnightCTF2024
