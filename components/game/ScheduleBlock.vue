<template>
    <div class="card card-plain">
        <Applications :games="games">
            <table class="schedule-table table" slot-scope="{enterOrCancel, isApplied, cancel, enter}">
                <thead>
                <tr>
                    <th width="15%" class="align-left">Date</th>
                    <th width="15%" class="align-left">Time</th>
                    <th width="5%" class="align-left">Duration</th>
                    <th width="50%" class="align-left">Showing</th>
                    <th width="20%" class="align-left"></th>
                </tr>
                </thead>
                <tbody>
                <tr class="schedule-block" v-for="game in limitBy(games, count)" :key="game.id" v-if="filter ? (filter === game.name) : true">
                    <td>
                        <div class="schedule-block__dow">{{ game.timestamp | moment('dddd') }}</div>
                        <div class="schedule-block__date">{{ game.timestamp | moment('MMMM D') }}</div>
                    </td>
                    <td>
                        <div class="schedule-block__time">{{ game.timestamp | moment('H:mm') }} UTC</div>
                    </td>
                    <td>
                        <div class="schedule-block__duration">{{ durations[game.name] || '30' }}</div>
                    </td>
                    <td>
                        <div class="schedule-block__show">DevWars Live</div>
                        <div class="schedule-block__title">{{ description(game)}}</div>
                    </td>
                    <td>
                        <a v-show="!isApplied(game)" @click="enter(game)" class="btn btn-primary">
                            Register for Entry
                        </a>
                        <a
                            v-show="isApplied(game)" @click="cancel(game)"
                            class="btn btn-outline-danger"
                        >Resign</a>
                    </td>
                </tr>
                </tbody>
            </table>
        </Applications>
    </div>
</template>

<script>
    import Component, { State } from 'nuxt-class-component';
    import Vue from 'vue';

    import { sortBy } from 'lodash';

    import { Prop } from 'vue-property-decorator';

    import Applications from '~/components/game/Applications';
    import GameDurations from '../../utils/game-durations';

    @Component({
        components: { Applications }
    })
    export default class ScheduleBlock extends Vue {
        @Prop({ default: '' }) filter;
        @Prop() count;

        durations = GameDurations;

        @State(state => state.game.upcoming) _games;

        get games() {
            return sortBy(this._games, game => game.timestamp);
        }

        description(game) {
            const descriptions = {
                'Classic': 'Classic - 3 VS 3',
                'Zen Garden': 'Zen Garden : 1 VS 1',
                'Blitz': 'Blitz - 1 VS 1',
            };

            return descriptions[game.name] || '';
        }
    }
</script>
