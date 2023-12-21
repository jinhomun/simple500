## README 생성
`echo "" > README.md`

## client
src 폴더에 App.js, index.css , index.js 제외하고 나머지 삭제
<div id="root"></div>


화살표 폴더일때,   
`rm -rf .git` 숨긴.git 파일 삭제하고,   
`git rm --cached . -rf` 캐쉬 초기화 하고   
`git add .`    
`git commit -m "dd"`   
`git push -u origin main`  

## client
npx create-react-app .   
npm install sass   
npm install react-bootstrap bootstrap   
npm install react-router-dom   
npm install axios   
npm install http-proxy-middleware   
npm install @emotion/css    
npm install @emotion/react  
npm install @emotion/styled   
npm install firebase   
npm install react-redux   
npm install @reduxjs/toolkit    
npm install react-avatar    
npm install moment  // 시간   

## server
npm init -y;   
npm install express --save;   
npm install nodemon --save;   
npm install path --save;   
npm install mongoose --save;   
npm install multer --save;      
npm install aws-sdk@2.348.0 --save;      
npm install multer-s3@2.10.0 --save;      

## 문제 해결
- client 폴더에 화살표 생길 때 : .git 폴더를 지운다.   
`rm -rf .git`   
`git rm --cached . -rf`# simple300   


## 제작과정
package.json -> main: index.js 파일 생성후 <br>
```js
const express = require("express");
const app = express();
const port = 5050;

app.listen(port, () => {
    console.log("running -->" + port);
})

app.get("/", (req, res) => {
    res.send("Hello World");
})

server를 오픈하면 "hello world" 문구뜸.
```

## nodemon 실행하기 위해선 start 셋팅
```js
{
  "name": "server",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "nodemon index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^8.0.1",
    "nodemon": "^3.0.1",
    "path": "^0.12.7"
  }
}


```

## client + server 
``` js
const express = require("express");
const path = require("path");
const app = express();
const port = 5050;

app.use(express.static(path.join(__dirname, "../client/build")));
app.listen(port, () => {
    console.log("running -->" + port);
})


app.get("/", (req, res) => {
    res.send("Hello World");
})

app.get("/sub", (req, res) => {
    res.sendFile(path.join(__dirname, "../client/build/index.html"));
})
```

## mongooose
```js
// mongodb+srv://answlsgh95:UGG7QMfWPOyW3UpV@cluster0.xlsy4ku.mongodb.net/?retryWrites=true&w=majority

const express = require("express");
const path = require("path");
const mongoose = require('mongoose');

const app = express();
const port = 5050;

app.use(express.static(path.join(__dirname, "../client/build")));
app.listen(port, () => {
    mongoose
        .connect(
            "mongodb+srv://answlsgh95:UGG7QMfWPOyW3UpV@cluster0.xlsy4ku.mongodb.net/?retryWrites=true&w=majority"
        )
        .then(() => {
            console.log("running -->" + port);
            console.log("connecting --> mongDB.....");
        })
        .catch((err) => {
            console.log(err)
        })
})



app.get("/", (req, res) => {
    res.send("Hello World");
})

app.get("/sub", (req, res) => {
    res.sendFile(path.join(__dirname, "../client/build/index.html"));
})
```
### 입력박스에 내용넣고 버튼누르면 출력하는 법
```js
import React, { useState } from 'react'


const App = () => {
  const [content, setContent] = useState("");

  const onSubmit = () => {
    alert(content);
  }

  return (
    <div>
      <h1>React</h1>
      <div>

      </div>
      <input
        type='text'
        value={content}
        onChange={(e) => {
          console.log(e)
          console.log(e.currentTarget.value)
          setContent(e.currentTarget.value);
        }}
      /><br />
      <button
        onClick={() => {
          onSubmit();
        }}
      >입력</button>
    </div >
  )
}

export default App
```

### 입력한 데이터 출력
```js
import React, { useState } from 'react'


const App = () => {
  const [content, setContent] = useState("");
  const [contentList, setContentList] = useState([]);

  const onSubmit = () => {
    let tempArr = [...contentList];
    tempArr.push(content)
    setContentList([...tempArr]);
  }

  return (
    <div>
      <h1>React</h1>
      <div>
        {contentList.map((content, key) => (
          <div key={key}>{content}</div>
        ))}
      </div>
      <input
        type='text'
        value={content}
        onChange={(e) => {
          console.log(e)
          console.log(e.currentTarget.value)
          setContent(e.currentTarget.value);
        }}
      /><br />
      <button
        onClick={() => {
          onSubmit();
        }}
      >입력</button>
    </div >
  )
}

export default App
```

### Upload에 입력하면 list에 저장되는방법
1.App.js<br>
```js
import React, { useState } from 'react'
import { Route, Routes } from 'react-router-dom'
import List from './components/List'
import Upload from './components/Upload'
import Heading from './components/Heading'

const App = () => {
  const [contentList, setContentList] = useState([]);
  return (
    <>
      <Heading />
      <Routes>
        <Route path='/list' element={<List contentList={contentList} setContentList={setContentList} />} />
        <Route path='/upload' element={<Upload contentList={contentList} setContentList={setContentList} />} />
      </Routes>
    </>
  )
}

export default App
```
2.Heading.js<br>
```js
import React from 'react'
import { Link } from 'react-router-dom'

const Heading = () => {
    return (
        <div>
            <h1>Hello React</h1>
            <Link to="/">Home</Link>
            <Link to="/upload">upload</Link>
            <Link to="/list">list</Link>
        </div>
    )
}

export default Heading
```

3.List.js <br>
```js
import React from 'react'

const List = (props) => {
    return (
        <div>
            {props.contentList.map((content, key) => (
                <div key={key}>
                    내용 : {content}
                </div>
            ))}
        </div>
    )
}

export default List
```
4.Upload.js <br>
```js
import React, { useState } from 'react'


const Uplaod = (props) => {
    const [content, setContent] = useState("");

    const onSubmit = () => {
        let tempArr = [...props.contentList];
        tempArr.push(content)
        props.setContentList([...tempArr]);
        setContent("");
    }
    return (
        <div>
            <input
                type='text'
                value={content}
                onChange={(e) => {
                    setContent(e.currentTarget.value);
                }}
            />
            <br />
            <button
                onClick={() => {
                    onSubmit();
                }}
            >입력</button>
        </div >
    )
}

export default Uplaod
```
5. header.js(React bootstrap에서 이용해서 Navbar가져옴)
```js
import React from 'react'
import { Navbar, Container, NavDropdown, Nav } from "react-bootstrap";

const Header = () => {
    return (
        <Navbar expand="lg" className="bg-body-tertiary">
            <Container>
                <Navbar.Brand href="#home">React-Bootstrap</Navbar.Brand>
                <Navbar.Toggle aria-controls="basic-navbar-nav" />
                <Navbar.Collapse id="basic-navbar-nav">
                    <Nav className="me-auto">
                        <Nav.Link href="/">Home</Nav.Link>
                        <Nav.Link href="/list">list</Nav.Link>
                        <Nav.Link href="/upload">upload</Nav.Link>
                        <NavDropdown title="Dropdown" id="basic-nav-dropdown">
                            <NavDropdown.Item href="/">Home</NavDropdown.Item>
                            <NavDropdown.Item href="/list">list</NavDropdown.Item>
                            <NavDropdown.Item href="/upload">upload</NavDropdown.Item>
                        </NavDropdown>
                    </Nav>
                </Navbar.Collapse>
            </Container>
        </Navbar>
    )
}

export default Header
```
6. header.js css 적용 --> client --> public --> index.html
```js
<!DOCTYPE html>
<html lang="ko">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>

  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css"
    integrity="sha384-9ndCyUaIbzAi2FUVXJi0CjmCapSmO7SnpJef0486qhLnuZ2cdeRhO02iuK6FUUVM" crossorigin="anonymous" />
</head>

<body>
  <div id="root"></div>
</body>

</html>
```

## setupProxy.js
```js
const { createProxyMiddleware } = require('http-proxy-middleware');

module.exports = function (app) {
    app.use(
        '/api',
        createProxyMiddleware({
            target: 'http://localhost:5050',
            changeOrigin: true,
        })
    );
};
```

## BrowserRouter
```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

import { BrowserRouter } from "react-router-dom";


const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

## list.js
```js
import React, { useEffect, useState } from 'react'
import axios from "axios";

const List = () => {
    const [text, setText] = useState("");
    useEffect(() => {
        let body = {
            text: "다시 보낸다. 잘 받아라!"
        }
        axios
            .post('/api/test', body)
            .then((response) => {
                setText(response.data.text)
                console.log(response);
            })
            .catch((error) => {
                console.log(error);
            });
    }, [])
    return (
        <div>
            <h3>{text}</h3>
        </div>
    )
}

export default List
```

## 업로드한 글을 list에 나오도록 하는방법
```js
const express = require("express");
const path = require("path");
const mongoose = require("mongoose");

const app = express();
const port = 5050;

app.use(express.static(path.join(__dirname, "../client/build")));
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

const { Post } = require("./Model/Post.js");

// mongodb+srv://answlsgh95:<password>@cluster0.xlsy4ku.mongodb.net/?retryWrites=true&w=majority

app.use(express.static(path.join(__dirname, "../client/build")));

app.listen(port, () => {
    mongoose.connect(
        "mongodb+srv://answlsgh95:UGG7QMfWPOyW3UpV@cluster0.xlsy4ku.mongodb.net/reactBlog?retryWrites=true&w=majority"
    )
        .then(() => {
            console.log("listening -->" + port);
            console.log("mongoose connecting...");
        })
        .catch((err) => {
            console.log(err)
        })
})

app.get("/", (req, res) => {
    res.sendFile(path.join(__dirname), "../client/build/index.html");
})

app.get("*", (req, res) => {
    res.sendFile(path.join(__dirname), "../client/build/index.html");
})

app.post("/api/post/submit", (req, res) => {
    let temp = req.body;
    console.log(temp);

    const BlogPost = new Post(temp);
    BlogPost.save().then(() => {
        res.status(200).json({ success: true })
    })
        .catch((err) => {
            console.log(err)
            res.status(400).json({ success: true })
        })
})

app.post("/api/post/list", (req, res) => {
    Post.find().exec()
        .then((doc) => {
            res.status(200).json({ success: true, postList: doc })
        })
        .catch((err) => {
            console.log(err);
            res.status(400).json({ success: false })
        })
})
```
```js
import React, { useEffect, useState } from 'react'
import axios from "axios";

const List = () => {
    const [postList, setPostList] = useState([]);

    useEffect(() => {
        axios.post('/api/post/list')
            .then((response) => {
                if (response.data.success) {
                    setPostList([...response.data.postList])
                }
            })
            .catch((err) => {
                console.log(err);
            })
    }, [])
    return (
        <div>
            <h3>글 목록</h3>
            {postList.map((post, key) => (
                <div key={key}>
                    <h3>제목: {post.title}</h3>
                    <p>내용: {post.content}</p>
                </div>
            ))}
        </div>
    )
}

export default List
```
```js
import React, { useState } from 'react'
import { useNavigate } from 'react-router-dom';

import { UploadButtonDiv, UploadDiv, UploadTitle, UploadForm } from '../style/UploadCSS.js'
import axios from 'axios';

const Upload = () => {
    const [title, setTitle] = useState("");
    const [contents, setContents] = useState("");
    let navigate = useNavigate();

    const onSubmit = () => {
        if (title === "" || contents === "") {
            return alert("제목과 내용을 채워주세요!");
        }

        let body = {
            title: title,
            content: contents,
        }

        axios.post("/api/post/submit", body)
            .then((response) => {
                if (response.data.success) {
                    alert("글 작성이 완료되었습니다.")
                    navigate('/list');
                } else {
                    alert("글 작성이 실패하였습니다.")
                }
            })
            .catch((err) => {
                console.log(err);
            })
    }
    return (
        <UploadDiv>
            <UploadTitle>Upload</UploadTitle>
            <UploadForm>
                <label>제목</label>
                <input
                    type="text"
                    id="title"
                    value={title}
                    onChange={(event) => {
                        setTitle(event.currentTarget.value);
                    }} /><br />

                <label htmlFor='contents'>내용</label>
                <textarea
                    type="text"
                    id="contents"
                    value={contents}
                    onChange={(event) => {
                        setContents(event.currentTarget.value);
                    }} /><br />

                <UploadButtonDiv>
                    <button
                        onClick={(e) => {
                            onSubmit(e);
                        }}
                    >제출
                    </button>
                </UploadButtonDiv>
            </UploadForm>
        </UploadDiv>
    )
}

export default Upload
```

## firebase 회원가입 데이터 들어가게 하는방법
새 프로젝트 --> 이름--> 권장 해지 --> 만들기 <br>

웹(</>) --> Client에다가  npm install firebase 설치 <br>

firebase.js폴더에 넣기
```js
import firebase from "firebase/compat/app";
import "firebase/compat/auth";

const firebaseConfig = {
    apiKey: "AIzaSyCgWVl7lk4_ImolhBj5k3D7GulUm-bj6iI",
    authDomain: "kickoff-90.firebaseapp.com",
    projectId: "kickoff-90",
    storageBucket: "kickoff-90.appspot.com",
    messagingSenderId: "453819675284",
    appId: "1:453819675284:web:8fd10e4206cddb605aba81"
};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);

export default firebase;
```
