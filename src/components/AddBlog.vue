<template>
    <div id="add-blog">
        <h2>添加博客</h2>

        <form v-if="!submitted">
            <label>博客标题</label>
            <input
                type="text"
                v-model="blog.title"
                required
                class="blog-title"
            />
            <label>博客内容</label>
            <textarea v-model="blog.content"></textarea>

            <div id="checkboxes">
                <input
                    type="checkbox"
                    value="Vue.js"
                    v-model="blog.categories"
                />
                <label>Vue.js</label>

                <input
                    type="checkbox"
                    value="Node.js"
                    v-model="blog.categories"
                />
                <label>Node.js</label>

                <input
                    type="checkbox"
                    value="React.js"
                    v-model="blog.categories"
                />
                <label>React.js</label>

                <input
                    type="checkbox"
                    value="Angular4"
                    v-model="blog.categories"
                />
                <label>Angular4</label>
            </div>

            <label>作者:</label>
            <select v-model="blog.author">
                <option v-for="author in authors" :key="author">
                    {{ author }}
                </option>
            </select>

            <button @click.prevent="postBlog">添加博客</button>
        </form>

        <div v-if="submitted">
            <h3>您的博客发布成功!</h3>
        </div>

        <div id="preview">
            <h3>博客总览</h3>
            <p>博客标题: {{ blog.title }}</p>
            <p>博客内容:</p>
            <p>{{ blog.content }}</p>
            <p>博客分类:</p>
            <ul>
                <li v-for="category in blog.categories" :key="category">
                    {{ category }}
                </li>
            </ul>
            <p>作者: {{ blog.author }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "add-blog",
    data() {
        return {
            blog: {
                title: "",
                content: "",
                categories: [],
                author: "",
            },
            authors: ["Eward", "Tim", "Bob"],
            submitted: false,
        };
    },
    methods: {
        postBlog: function () {
            this.$http
                .post(
                    "https://myblog-2be6a-default-rtdb.asia-southeast1.firebasedatabase.app/posts.json",
                    this.blog
                )
                .then(function (data) {
                    // 请求成功
                    console.log(data);
                    this.submitted = true;
                });
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* 所有元素, 设置的边框和内边距的值是包含在width内的 */
#add-blog * {
    box-sizing: border-box;
}

/* 设置页面边距, 外边距为20 */
#add-blog {
    margin: 20px auto;
    max-width: 600px;
    padding: 20px;
}

label {
    display: block;
    margin: 20px 0 10px;
}

input [type="text"],
textarea,
select {
    display: block;
    width: 100%;
    padding: 8px;
}

.blog-title {
    height: 30px;
}

textarea {
    height: 300px;
}

#checkboxes label {
    display: inline-block;
    margin-top: 0;
}

#checkboxes input {
    display: inline-block;
    margin-left: 30px;
}

button {
    display: block;
    margin: 20px 0;
    background: crimson;
    color: whitesmoke;
    border: 0;
    padding: 12px;
    border-radius: 4px;
    font-size: 17px;
    cursor: pointer;
}

#preview {
    padding: 10px 20px;
    border: 1px dotted #ccc;
    margin: 30px 0;
}

h3 {
    margin-top: 10px;
}
</style>
