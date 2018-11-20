# python3 的坑
1. Flask跨域的问题
    - 解决方案：
        1. 下载flask_cors包
        ```python
        pip3 install flask-cors
        ```
        - 使用flask_cors的CORS，代码示例：
        ```python
        from flask_cors import *
        app = Flask(__name__)
        CORS(app, supports_credentials=True)
        ```