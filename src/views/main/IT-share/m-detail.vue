<style>
	.container-m .blog-detail {
		width: 90%;
	    margin: 0 auto;
	    overflow: hidden;
	    line-height: 22px;
	}
	.container-m h4.article {
		font-size: 16px;
		color: #fff;
    	margin-bottom: 30px;
     	text-align: center; 
	}
	.container-m .blog-detail ul p {
		color: #fff;
		margin-bottom: 20px;
		text-align: left;
		font-size: 14px;
	}
	.container-m .blog-detail ul p img{
		max-width: 100%;
		height: auto;
	}
	.container-m .blog-detail ul {
		padding: 0;
		margin: 0;
	}
</style>

<template>
	<section>
		<article class="m-IT"   v-loading="loading"  element-loading-text="拼命加载中"  element-loading-spinner="el-icon-loading" element-loading-background="rgba(180, 180, 180, 0.8)">
			<div class="container-m">
				<div class="blog-detail">
					<ul>
						<h4 class="article">
							<div>{{detail.title}}</div>
							<span style="float: right;font-size: 13px;padding-top: 4px;">{{detail.time}}</span>
						</h4>
						<div v-html="detail.content"></div>
						<p>
						    (本文由前端工程师steven沈文杰原创，转载请放原文链接，谢谢！)
						</p>
						<p style="text-align: center;color: #3ae810">#个人原创，难免有错误之处，欢迎各位留言批评指正! 谢谢!#</p>
						<div style="text-align: center;margin-bottom: 12px;">
							<el-button type="success" @click="goBack()" round>返回</el-button>
						</div>
					</ul>
				</div>
			</div>
		</article>
	</section>
</template>



<script>
    export default {
    	data () {
    		return {
    			detail: {
    				loading: false,
    				title: '',
    				content: '',
    				time: ''
    			}
    		}
    	},
    	methods: {
    		getArticleDetail() {
	    		// 获取文章详情
	    		this.loading = true;
	    		this.$http.get('src/phpCtrl/articleDetail.php', {
	    			params: {
	    				id: this.$route.query.id
	    			}
	    		}).then(res => {
	    			this.detail.title = res.data.title;
	    			this.detail.content = res.data.content;
	    			this.detail.time = res.data.createTime;
	    			this.loading = false;
	    		}).catch(err => {
	    			this.$message.error('获取文章详情失败!');
	    			console.log(err)
	    		});
    		},
    		goBack () {
    			this.$router.go(-1);
    		}
    	},
    	created () {
    		this.getArticleDetail();
    	}
    };
</script>