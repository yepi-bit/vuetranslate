<template>
	<div>
		<h1>Yepi在线翻译</h1>
		<div class="box">
			<div class="clsOperation">
				<a-select v-model:value="language" show-search style="width: 200px" :options="options">
				</a-select>
				<a href="javascript:void(0)" class="exchange">
					<SwapOutlined />
				</a>
				<a-select v-model:value="toLanguage" show-search style="width: 200px" :options="options">
				</a-select>
				<a-button class="btnTranslate" type="primary" @click="translateText">翻译</a-button>
			</div>
			<div>
				<a-row>
					<a-col :span="12">
						<a-textarea v-model:value="translate" placeholder="请输入要查询的文字" :rows="8" />
					</a-col>
					<a-col :span="12">
						<a-textarea class="bgColor" v-model:value="translate" :rows="8" />
					</a-col>
				</a-row>
			</div>
			<div class="magnifier-container">
				<a-row :gutter="20">
					<a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
						<a-card shadow="hover">
							<div><span>放大镜1</span></div>
							<vab-magnifier url="https://picsum.photos/960/540?random=1" type="circle"></vab-magnifier>
						</a-card>
					</a-col>
					<a-col :xs="24" :sm="24" :md="24" :lg="12" :xl="12">
						<a-card shadow="hover">
							<div><span>放大镜2</span></div>
							<vab-magnifier url="https://picsum.photos/960/540?random=2" type="square"></vab-magnifier>
						</a-card>
					</a-col>
				</a-row>
			</div>
		</div>
	</div>
</template>
<script>
	import axios from 'axios'
	import VabMagnifier from 'zx-magnifie'
	import {
		SwapOutlined
	} from '@ant-design/icons-vue';
	import {
		ref
	} from 'vue'
	export default {
		name: 'App',
		components: {
			SwapOutlined,
			VabMagnifier
		},
		setup() {
			const translate = ref('')
			const language = ref('自动检测')
			const toLanguage = ref('中文(简体)')
			const options = ref([{
					value: '中文',
					label: '中文'
				},
				{
					value: '英语',
					label: '英语'
				},
				{
					value: '韩语',
					label: '韩语'
				},
			]);
			const translateText = () => {
				axios.post(
						'api/trasnslate_o?smartresult=dict&smartresult=rule')
					.then((response) => {
						console.log(response)
						this.translatedText = response.body.text[0];
					})
			}
			return {
				translate,
				language,
				options,
				toLanguage,
				translateText
			}
		}
	}
</script>
<style>
	h1 {
		padding: 24px;
		letter-spacing: 8px;
		text-align: center;
		font-weight: 700;
	}

	.box {
		width: 100%;
		padding: 24px 280px;
		margin: 0 auto;
	}

	.clsOperation {
		margin-bottom: 18px;
	}

	.bgColor {
		background-color: rgb(242, 242, 242) !important;
	}

	.exchange {
		padding: 24px;
	}

	.btnTranslate {
		width: 106px;
		font-weight: 400;
		text-indent: 8px;
		margin-left: 24px;
		letter-spacing: 8px;
		border-radius: 6px !important;
	}
</style>
