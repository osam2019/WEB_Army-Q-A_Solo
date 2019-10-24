<template>
    <div id="app">
        <span class="headline">새 글 등록하기</span>
        <el-input
                type="textarea"
                autosize
                placeholder="제목을 입력하세요"
                v-model="titleArea">
        </el-input>
        <div style="margin: 20px 0;"></div>
        <el-input
                type="textarea"
                :autosize="{ minRows: 5, maxRows: 30}"
                placeholder="내용을 입력하세요"
                v-model="contentArea">
        </el-input>

        <div class="write"><el-button type="primary" icon="el-icon-edit" @click="write_push">작성하기</el-button></div>
    </div>
</template>

<script>
    import * as boardActions from "@/store/modules/board/types";
    import {mapActions, mapGetters, mapState} from "vuex";
    import state from "@/store/modules/board/state";

    export default {
        name: "app",
        data() {
            return {
                titleArea: '',
                contentArea: ''
            }
        },
        computed: {
            ...mapState({
                items({board}) {
                    console.log("state ", board);
                    //console.log("DDD test111 ", board.items)
                    return board.items;
                }
            })
        },
        methods: {
            write_push() {
                if (this.titleArea != '' && this.contentArea != '') {
                        this[boardActions.ADD_POST]({
                            newTitle: this.titleArea,
                            newContent: this.contentArea
                        });
                    this.$message('새 글이 등록되었습니다.');
                } else {
                    this.$message('제목과 내용은 비울 수 없습니다.');
                }
            }
        }
    }
</script>

<style scoped>
    .headline {
        display: inline-block;
        font-weight: bold;
        font-size: 22pt;
        color: #aaaaaa;
        margin: 50px;
    }
    .write {
        display: inline-block;
        margin: 50px;
    }
</style>