<style lang="less">
    @import '../../../styles/common.less';
</style>

<template>
    <Card>
        <single-table ref="table"
                      :columns="table.columns"
                      form-title="应用客户端维护"
                      domain-url="oauthClient"
                      :label-width="100"
                      :form-rule="form.rule"
                      :form-data="form.data">
            <template slot="query-form" slot-scope="props">
                <FormItem class="padding-right-medium" prop="loginName" label="登录名">
                    <Input v-model="props.params.loginName" placeholder="登录名"/>
                </FormItem>
                <FormItem class="padding-right-medium" prop="name" label="姓名">
                    <Input v-model="props.params.name" placeholder="姓名"/>
                </FormItem>
                <FormItem class="padding-right-medium" prop="roleId" label="角色">
                    <label>
                        <Select v-model="props.params.roleId">
                            <Option v-for="role in roles" :value="role.id" :key="role.id">{{role.name}}</Option>
                        </Select>
                    </label>
                </FormItem>
            </template>

            <template slot="edit-form" slot-scope="props">
                <FormItem label="名称" prop="name">
                    <Input v-model="props.data.name" placeholder="请输入名称"/>
                </FormItem>
                <FormItem label="resource_ids" prop="resourceIds">
                    <Input v-model="props.data.resourceIds" placeholder="请输入resource_ids"/>
                </FormItem>
                <FormItem label="client_id" prop="clientId">
                    <Input v-model="props.data.clientId" placeholder="请输入client_id"/>
                </FormItem>
                <FormItem label="client_secret" prop="clientSecret">
                    <Input v-model="props.data.clientSecret" placeholder="请输入clientSecret"/>
                </FormItem>
                <FormItem label="scope" prop="scope">
                    <Input v-model="props.data.scope" placeholder="请输入scope"/>
                </FormItem>
                <FormItem label="grant_types" prop="authorizedGrantTypes">
                    <Input v-model="props.data.authorizedGrantTypes" placeholder="请输入grant_types"/>
                </FormItem>
                <FormItem label="redirect_uri" prop="webServerRedirectUri">
                    <Input v-model="props.data.webServerRedirectUri" placeholder="请输入redirect_uri"/>
                </FormItem>
            </template>
        </single-table>
    </Card>
</template>

<script>
    import util from '@/libs/util';
    import singleTable from '@/views/my-components/single-table/single-table.vue';

    export default {
        components: {
            singleTable
        },
        data() {
            return {
                table: {
                    columns: [
                        {key:'name', title:'名称'},
                        {key:'clientId', title:'client_id'},
                        {key:'clientSecret', title:'client_secret'}
                    ]
                },
                form: {
                    rule: {
                        name: [
                            { required: true, message: '请填写名称', trigger: 'blur' }
                        ],
                        resourceIds: [
                            { required: true, message: '请填写resource_ids', trigger: 'blur' }
                        ],
                        clientId: [
                            { required: true, message: '请填写clientId', trigger: 'blur' }
                        ],
                        clientSecret: [
                            { required: true, message: '请填写clientSecret', trigger: 'blur' }
                        ],
                        scope: [
                            { required: true, message: '请填写scope', trigger: 'blur' }
                        ],
                        authorizedGrantTypes: [
                            { required: true, message: '请填写authorizedGrantTypes', trigger: 'blur' }
                        ]
                    },
                    data: {
                        id: null,
                        name: null,
                        resourceIds: null,
                        clientId: null,
                        clientSecret: null,
                        scope:null,
                        authorizedGrantTypes:null,
                        webServerRedirectUri:null
                    }
                },
                roles: []
            }
        },
        methods: {
        },
        mounted() {
            this.$refs.table.loadGrid();
        }
    };
</script>