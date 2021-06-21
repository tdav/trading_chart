<script>
 
import { Overlay } from 'trading-vue-js'

export default {
    name: 'TestOverlay',
    mixins: [Overlay],
    methods: {
        meta_info() {
            return { author: 'CyberFist', version: '1.0.0' }
        },
         
        draw(ctx) {
            ctx.lineWidth = this.line_width
            ctx.strokeStyle = this.color
            ctx.beginPath()

            const layout = this.$props.layout
            const i = this.data_index

            for (var p of this.$props.data) {
                let x = layout.t2screen(p[0])
                let y = layout.$2screen(p[i])
                ctx.lineTo(x, y)
            }
            ctx.stroke()
        },

       
        use_for() { return ['TestOverlay'] },

       
        data_colors() { return [this.color] }
    },
    // Define internal setting & constants here
    computed: {
        sett() {
            return this.$props.settings
        },
        line_width() {
            return this.sett.lineWidth || 3
        },
        color() {
            const n = this.$props.num % 5
            return this.sett.color || this.COLORS[n]
        },
        data_index() {
            return this.sett.dataIndex || 1
        }
    },
    data() {
        return {
            COLORS:
            [
                '#5691ce', '#612ff9',
                '#d50b90', '#ff2316'
            ]
        }
    }

}
</script>
