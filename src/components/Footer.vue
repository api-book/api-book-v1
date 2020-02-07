<template>
    <footer class="c-footer">
        <p class="c-footer-links">
            <a
                v-for="(info, key) in social"
                :href="info.url"
                :title="info.title"
                target="_blank"
                :key="key"
            >
                <i :class="'u-icon u-icon-' + key"></i>
            </a>
        </p>
        <p class="c-footer-copyright">
            &copy;{{ copyright.time }}
            <a :href="copyright.url" target="_blank">{{ copyright.site }}</a>
        </p>
    </footer>
</template>

<script>
export default {
    name: "Footer",
    data: function() {
        return {
            social: this.$root.setting.footer.social,
            copyright: this.$root.setting.footer.copyright
        };
    }
};
</script>

<style lang="less">
@import '../assets/css/var.less';
.c-footer {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    text-align: center;
    padding-top: 20px;
    padding-bottom: 25px;
    font-size: 12px;
}
.c-footer-copyright {
    a {
        color: @link;
    }
    a:hover {
        color: @pink;
        box-shadow: 0 1px 0 @pink;
    }
}
.c-footer-links {
    a {
        padding: 0 9px;
    }
    .u-icon-email {
        width: 12px;
        height: 12px;
    }
    .u-icon-weibo {
        width: 12px;
        height: 12px;
    }
    .u-icon-wechat {
        width: 12px;
        height: 12px;
    }
    margin-bottom: 8px;
}
</style>
